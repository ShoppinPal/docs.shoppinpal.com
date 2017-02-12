# Role Resolvers
Use `Role.registerResolver()` to set up a custom role handler in a boot script. This function takes two parameters: 

1. String name of the role in question.
2. Function that determines if a principal is in the specified role. The function signature must be `function(role, context, callback)`.

##### Example
```
module.exports = function(app) {
  var _ = require('underscore');
  var Role = app.models.Role;
  Role.registerResolver(adminForOrg, function(role, context, cb) {
    function reject(err) {
      if(err) {
        return cb(err);
      }
      cb(null, false);
    }
    if(context.modelName !== 'Organisation'){
      // return error if target model is not organisation
      return reject();
    }
    var currentUserId = context.accessToken.userId;
    var currentOrg = context.modelId;
    if(!currentUserId){
      // Do not allow unauthenticated users to proceed
      return reject();
    }
    if(!currentOrg){
      return reject();
    }
    else {
      app.models.User.findById(currentUserId, {include:
        {
          relation:'roles',
          scope : {
            fields: ['name'] // only include the role name and id
          }
        }
      })
      .then(function(userModelInstance){
       var isAdmin = _.findWhere(currentUserRoles,{name: 'orgAdmin'});
        if(!_.isEqual(userModelInstance.organisationId.toString(),currentOrg.toString()) || !isAdmin){
          return reject(); // reject if the user's org isn't the current org
        }
        else {
          return cb(null,true);
        }
      })
      .catch(function(error){
        cb(error);
      });
    }
  });
});
```