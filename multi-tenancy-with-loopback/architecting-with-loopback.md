#Multi Tenant Architecture with Loopback
![](/assets/multi-tenant-architecture.png)

We define [loopback models](https://loopback.io/doc/en/lb3/Defining-models.html) for achieving multi tenancy in a way that every specific model passes through organization model and is data accessible is only specific to particular organization. 

We restrict access to every direct methods for each model and only make them accessible through organization model such that only org specific data could be returned.

###Define models and their base
In loopback when you create a model with the model generator, you choose a base model, that is, the model that your model will “extend” and from which it will inherit methods and properties. [Read more about models](https://loopback.io/doc/en/lb3/Extending-built-in-models.html)

Since user model is the most restricted and protected model which makes it difficult to hack  into un-authorized data, we chose it to be the base for our organization model.



#####Relationships
* Users -> `Belongs To` - Organization
* Organization -> `Has Many` - Users


* Products -> `Belongs To` - Organization
* Organization -> `Has Many` - Products


* Catalog -> `Belongs To` - Organization
* Organization -> `Has Many` - Catalog


* Orders -> `Belongs To` - Organization
* Organization -> `Has Many` - Orders

#####Sample Queries 

1. Create product for Organization
```
Organization.prodcut.create({
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
```
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

#####Invalid or disabled Queries
Will give `401 Authorization Required` error as these will be disabled from the backend.

1. Create product for Organization
```
Prodcut.create({
    name: "Product-A",
    desc: "This product belongs to org-a"
})
```
2. Fetch product for Organization
```
Prodcut.find({
    where:{
        name: "Product-A"
    } 
}}
```

To read more about how to disable methods in loopback you can redirect to this [article](https://loopback.io/doc/en/lb3/Exposing-models-over-REST.html#exposing-and-hiding-models-methods-and-endpoints).





















