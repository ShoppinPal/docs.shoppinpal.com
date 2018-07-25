# Architecting with Loopback

![](../.gitbook/assets/multi-tenant-architecture.png)

We define [loopback models](https://loopback.io/doc/en/lb3/Defining-models.html) for achieving multi tenancy, such that every `Model` passes through organization model and the data accessible is only specific to particular organization.

We restrict access to all direct methods for each model and only make them accessible through organization model. This way, only org specific data could be returned.

## Define models and their base

In loopback when you create a model with the model generator, you choose a base model, that is, the model that your model will “extend” and from which it will inherit methods and properties. [Read more about models](https://loopback.io/doc/en/lb3/Extending-built-in-models.html)

Since `user` model is the most restrictive and protected model, it is difficult to hack into unauthorized data, we chose it to be the base for our organization model.

Also the [concept](https://github.com/strongloop/loopback/issues/854#issuecomment-63992641) of `$owner` ACLs only works for `user` models and its inheritors, so that is a huge technical reason for picking this model as well.

### Relationships

* Users -&gt; `Belongs To` - Organization
* Organization -&gt; `Has Many` - Users
* Products -&gt; `Belongs To` - Organization
* Organization -&gt; `Has Many` - Products
* Catalog -&gt; `Belongs To` - Organization
* Organization -&gt; `Has Many` - Catalog
* Orders -&gt; `Belongs To` - Organization
* Organization -&gt; `Has Many` - Orders

### Sample Queries

1. Create product for Organization

   ```text
   Organization.product.create({
    name: "Product-A",
    desc: "This product belongs to org-a"
   })
   .then(function(success){
    ...
   })
   .catch(function(err){
    ...
   });
   ```

2. Fetch product for Organization

   ```text
   Organization.prodcut.find({
    where:{
        name: "Product-A"
    } 
   })
   .then(function(success){
    ...
   })
   .catch(function(err){
    ...
   });
   ```

### Invalid or disabled Queries

Following samples will give `401 Authorization Required` error as these **should** be disabled from the backend.

1. Create product for Organization

   ```text
   Product.create({
    name: "Product-A",
    desc: "This product belongs to org-a"
   })
   ```

2. Fetch product for Organization

   ```text
   Prodcut.find({
    where:{
        name: "Product-A"
    } 
   }}
   ```

_Why?_ Remember, earlier we decided to:

> restrict access to all direct methods for each model and only make them accessible through organization model. This way, only org specific data can be returned.

To read more about how to disable methods in loopback you can refer to this [article](https://loopback.io/doc/en/lb3/Exposing-models-over-REST.html#exposing-and-hiding-models-methods-and-endpoints).

