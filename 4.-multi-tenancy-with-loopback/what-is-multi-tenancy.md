# What is Multi-Tenancy

1. Multiple Users/Tenants can belong to an organization.
2. We can have multiple organizations in the same server and db.
3. Any data created for the organization or any data created by the users of that organization should be segragated from the the users of another organization.
4. If we want, we should be able to configure the users that belong to the same organization to view any data which other users of that organization created.

## Industry Requirements

1. User of an organization can have different administrative roles and authorizations.
2. Organization can have different hierarchical powers defined for various set of users. 
3. Organization should have one or more `admin-user` who can control and define access for other users in the organization.
4. Organization may or may-not want their data to be shared with other organizations.

