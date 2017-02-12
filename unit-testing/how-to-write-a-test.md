# Unit Testing

## How to write a test

Everyone has the same question when writing tests for first time.
- You must break down the logic of your application into small chunks or units and verify that each chunk works perfectly and as desired.
- **In javascript the smallest individual chunk you can test is usually functions. The core feature in application must be verified with accompanying unit tests.**
- Unit testing must be done on the basis of input and output for an individual function so when functions are joined together, your code has a better chance to work as a whole.
- It is better not to interfere with the operation of a function.

Best practice says you should write your unit test before actual development starts. You must be questioning yourself, how can we possibly do that? The answer is simple: just create an empty unit test for the function, keep updating it when function is updated, and freeze it when final touches are made on that function's development. Now if any newcomers try to make changes in code, they would easily find out about any mistakes if & when the tests break.

Unit tests must be broken down into 3 parts:

1. Story
2. Feature
3. Units

So in our case Story is \`_Users come to our page and login, if successful they are redirected to Profile page_\`. In this we state that our feature is user login and we further divide this feature into units as follows:

1. Ensure invalid emails do not pass.
2. Ensure valid emails pass the validation.
3. Ensure path changes on user logged in.

```
describe("user login form", function() {
    it("Ensure invalid emails do not pass", function() {});
    it("Ensure valid emails pass the validation", function() {});
    it("Ensure path changes on user logged in", function() {});
});
```

