# Better Programming with multi-tenancy

Now when you have multi-tenancy applied in your project, its very important to write clean and modular code for easy understanding and improved readability. Here are some important suggestions to follow that will help you to write better code:

1. Since most of the methods you write will pass through organization and will often be defined in `organization.json`, make sure to define functions specific to particular models inside their own `model.json` and internally call the function with right arguments from `organization.json` file. Example:
   * Define the main function in `product.json` file 

     ```text
     Product.addProductsInBulk = function (id, data) {
       ....
       .... // function algorithm
       ....
       return promise;
     }
     ```

   * And expose a remote method in `organization.json` file, as a wrapper which calls `addProductsInBulk`:

     ```text
     Organisation.remoteMethod('addProducts', {
       accepts: [
           {arg: 'id', type: 'string', required: true},
           {arg: 'data', type: 'object', required: true, http: {source: 'body'}}
       ],
       http: {path: '/:id/products/add', verb: 'post'},
       returns: {arg:'products', type: 'object', root: true}
     });
     Organisation.addProducts = function (id, data, cb) {
       app.models.Product.addProductsInBulk(id, data)
       .then(function (response) {
           cb(null, response);
       })
       .catch(function(error){
           cb(error);
       });
     };
     ```

