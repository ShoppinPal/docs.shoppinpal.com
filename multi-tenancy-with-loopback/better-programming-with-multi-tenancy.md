#Improve Modularity
Now when you have multi-tenancy applied in your project its very important to write clean and modular code for easy understanding and improved readability. Here are some important suggestions to follow that will help you to write better code:

1. Since most of the methods you write will pass from organization and will often be defined in `organization.json` make sure to define function specific to particular model inside their own `model.json` and internally call the function with right arguments from `organization.json` file.
eg:

    * and define the main function in `product.json` file 
```
 Product.addProductsInBulk = function (id, data) {
     ....
     .... // function algorith
     ....
     return promise;
 }
```
    * And just make remothe method a wrapper to call `addProductsInBulk` from `organization.json` file.
        
    ```
    Organisation.remoteMethod('addProductsInBulk', {
    accepts: [
        {arg: 'id', type: 'string', required: true},
        {arg: 'data', type: 'object', required: true, http: {source: 'body'}}
        ],
        http: {path: '/:id/products/add', verb: 'post'},
        returns: {arg:'products', type: 'object', root: true}
    });
    Organisation.addProduct = function (id, data, cb) {
        app.models.Product.addProductsInBulk(id, data)
        .then(function (response) {
            cb(null, response);
        })
        .catch(function(error){
            cb(error);
        });
    };
    ```