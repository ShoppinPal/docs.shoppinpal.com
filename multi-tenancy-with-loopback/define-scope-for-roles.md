#Roles in Loopback
Loopback allows you to define various [User Roles](https://loopback.io/doc/en/lb3/Defining-and-using-roles.html) based on the requirements. It enables you to define both [static](https://loopback.io/doc/en/lb3/Defining-and-using-roles.html#static-roles) and [dynamic](https://loopback.io/doc/en/lb3/Defining-and-using-roles.html#dynamic-roles) roles. Static roles are stored in a data source and are mapped to users. In contrast, dynamic roles aren’t assigned to users and are determined during access.


###Multi-Tenant Roles 
1. An `orgAdmin` like role is required for access over REST to allow for administrative actions needed for any particular organization:
    1. API's to manage/invite other users,
    2. profile and payments configurations, and
    3. deciding hierarchal powers.
    4. Hopefully, it makes sense naturally that such actions *should* only be allowed for an organization's administrators.
2. An `orgUser` role is required for accessing other basic APIs which help an organization execute properly.

###Built In Roles
LoopBack enables you to define dynamic roles that are defined at run-time. 

LoopBack provides the following built-in dynamic role
`$owner` - Owner of the object
`$authenticated` - authenticated user
`$unauthenticated` - Unauthenticated user
`$everyone` - Everyone


###Define Custom Role
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

