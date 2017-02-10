#Multi-tenancy defined
A tenant(User) is any application -- either inside or outside the enterprise -- that needs its own secure and exclusive software environment. This environment can encompass all or some selected features of the software application, from storage to user interface.


#What does multi-tenant mean to us?
1. Multiple Users/Tenants can belong to an organization.
2. We can have multiple organizations in the same server and db.
3. Any data created for the organization or any data created by the users of that organization should be segragated from the the users of another organization.
4. If we want, we should be able to configure the users that belong to the same organization to view any data that other users of that organization created.