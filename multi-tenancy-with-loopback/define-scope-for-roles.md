#Roles and their resolvers
Loopback allows you to define various [User Roles](https://loopback.io/doc/en/lb3/Defining-and-using-roles.html) based on the requirements. It enables you to define both [static](https://loopback.io/doc/en/lb3/Defining-and-using-roles.html#static-roles) and [dynamic](https://loopback.io/doc/en/lb3/Defining-and-using-roles.html#dynamic-roles) roles. Static roles are stored in a data source and are mapped to users. In contrast, dynamic roles aren’t assigned to users and are determined during access.


###Multi-Tenant Roles 
1. A `orgAdmin` like role for access over REST is required to allow access for the administrative actions needed for any particular organization. Api's to manage/invite other users, profile and payments configurations and decide hierarchal powers were to be only allowed for organization admins.

2. `orgUser` role for access over other basic apis which helps organization to execute properly. 

###Built In Role resolvers
LoopBack enables you to define dynamic roles that are defined at run-time. 

LoopBack provides the following built-in dynamic role
`$owner` - Owner of the object
`$authenticated` - authenticated user
`$unauthenticated` - Unauthenticated user
`$everyone` - Everyone


###Custom Role definition
You can create custom role through boot scripts. Here's an example for creating custom role.

```
var Role = app.models.Role;
var RoleMapping = app.models.RoleMapping;

Promise.resolve()
.then(function () {
    return Role.findOrCreate(
        {where: {name: 'orgAdmin'}}, 
        {
            name: 'orgAdmin',
            description: 'admin of the org'
        }
    );
})
.then(function () {
    log.trace('Role created successfully');
    return cb();
})
.catch(function (error) {
    log.error('Error in creating roles', error);
    return cb(error);
});

```

