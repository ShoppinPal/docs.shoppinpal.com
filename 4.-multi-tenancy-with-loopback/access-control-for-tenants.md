# Access Control For Tenants

Once you have proper roles and role resolvers added into your project the next step comes to setup proper [access controls \(ACL\)](https://loopback.io/doc/en/lb2/Controlling-data-access.html) for REST apis.

You can setup the correct ACL for each built-in method or [remote methods](http://loopback.io/doc/en/lb3/Remote-methods.html) through javascript \(`<model>.js` files\) or you can add ACL rules in `<model>.json` file.

## Example

For example, lets setup some ACL rules in organization model for a custom method names `addProductsInBulk` through `organization.json` file

```text
...
"acls": [
        {
            "accessType": "EXECUTE",
            "principalType": "ROLE",
            "principalId": "adminForOrg",
            "permission": "ALLOW",
            "property": "addProductsInBulk"
        },
        {
            "accessType": "EXECUTE",
            "principalType": "ROLE",
            "principalId": "userForOrg",
            "permission": "ALLOW",
            "property": "addProductsInBulk"
        },
    ]
...
```

