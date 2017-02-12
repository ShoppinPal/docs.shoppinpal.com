# Unit Testing

## Writing tests

There are rules to write structured test projects:

1. Each module must contains its own tests for angular service, directive, factory, controller, component and filters.
2. Test must be inside test directory of each module.
3. It must have naming convention like _yourservice.\_spec.js or \_yourdirective_.spec.js etc.
4. And most important of all **do not forget to include the test directory in karma.conf file :\)**

Lets first write tests for login module in angular app. For simplicity of code I am taking three test cases for it.

1. Ensure invalid emails do not pass.
2. Ensure valid emails pass the validation.
3. Ensure path changes on user logged in.

> AngularJS also has the [`ngMock`](https://docs.angularjs.org/api/ngMock) module, which provides mocking for your tests. This is used to inject and mock AngularJS services within unit tests. In addition, it is able to extend other modules so they are synchronous. Having tests synchronous keeps them much cleaner and easier to work with. One of the most useful parts of ngMock is[`$httpBackend`](https://docs.angularjs.org/api/ngMock/service/$httpBackend) , which lets us mock XHR requests in tests, and return sample data instead.

Please open `client/app/login/test/controller.spec.js` file to see all test cases. Files are well documented.
