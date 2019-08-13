# Working with Transparent Data Encryption in SQL Server

The master database contains all of the system level information for SQL Server. It gets created when the server instance of SQL Server is created. Use master database to setup the master encryption key
`/opt/mssql-tools/bin/sqlcmd -S localhost -U sa -P 1Password! -d master -N -C -Q "CREATE MASTER KEY ENCRYPTION BY PASSWORD = ''1TestPassword!''"`{{execute T1}}

Create a certificate in the master database 
`/opt/mssql-tools/bin/sqlcmd -S localhost -U sa -P 1Password! -d master -N -C -Q "CREATE CERTIFICATE MyServerCert WITH SUBJECT = ''My Database Encryption Key Certificate''"`{{execute T1}}

Create a database called TestDB to be encrypted 
`/opt/mssql-tools/bin/sqlcmd -S localhost -U sa -P 1Password! -N -C -Q "CREATE DATABASE TestDB"`{{execute T1}}

Create database encryption key with AES_256 algorithm and encrypted by server certificate
`/opt/mssql-tools/bin/sqlcmd -S localhost -U sa -P 1Password! -d TestDB -N -C -Q "CREATE DATABASE ENCRYPTION KEY WITH ALGORITHM = AES_256 ENCRYPTION BY SERVER CERTIFICATE MyServerCert;"`{{execute T1}}

Turn ON database encryption
`/opt/mssql-tools/bin/sqlcmd -S localhost -U sa -P 1Password! -d TestDB -N -C -Q "ALTER DATABASE TestDB SET ENCRYPTION ON"`{{execute T1}}

List the databases that are encrypted. Encrypted_state = 3 means these databases are in encrypted state
`/opt/mssql-tools/bin/sqlcmd -S localhost -U sa -P 1Password! -d TestDB -N -C -Q "select a.name from sys.dm_database_encryption_keys b join sys.databases a on a.database_id = b.database_id where encryption_state = 3"`{{execute T1}}