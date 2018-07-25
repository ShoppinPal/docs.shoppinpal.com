# Nuances

## Differences between usage in nodejs vs angularjs

When we execute http requests calls from AngularJS services, usually we use $http which returns by default a promise object which we use like so:

```text
$http.get()
.$promise.then(function(){
});
```

Whereas in nodejs we can do:

```text
request.get()
.then(function(){
});
```

