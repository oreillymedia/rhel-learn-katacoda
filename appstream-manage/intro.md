# Goal:

After completing this scenario, users will be able to choose which version of a software package is enabled on a system from an application stream.

# Concepts included in this scenario:
* Verify the availability of an application stream
* Install software managed as an application stream
* Change to a different version of software from an application stream
* List all available software managed as application streams

# Example Usecase:

A web application being deployed on Red Hat Enterprise Linux 8 requires postgresql database version 9.6.  Later, the application is updated and requires postgresql version 10 be available on the machine.

**Please Note:** The instructions to move the database stored data from postgresql 9.6 to 10 are not included in this scenario, but would likely be needed if an administrator or developer was moving a production system from using postgresql 9.6 to postgresql 10.  Additional administrative activities may be required when performing a move from one version of software to another, including, but not limited to: scheduling a maintenance for the system, notifying users/stakeholders, backing up data, testing post-change, etc.

