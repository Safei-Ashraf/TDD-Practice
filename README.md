# some of my personal notes on my learning journy toward TDD and Cypress.


**mixed up from different resources, all mentioned at the end ot this section, followed by README for the practice project.**


##  TDD Ref: https://outsidein.dev/



some of the common agile development practices:(mostly development practices) 


• Small Stories: we break the work up into minimum units of user-visible functionality.
		○ For example, rather than building out the entire data layer at once, we build out just enough of the data later to get one feature working, along with the corresponding business logic and user interface. We finish that work and make it available for review. Then we start the next story, and add another slice of data layer, business logic, and user interface.
		
	• Evolutionary Design: as we're adding this functionality story-by-story, we don't try to think ahead for everything our application will need and design an architecture that will accommodate it—because we know we'll be wrong. Instead, we strive to make the system the best design for its functionality as it stands today, for this story. When the next story starts, then we adjust the design of the system to match the new functionality. As a result of making these changes, we should never have a system that is either underdesigned with hacked-in changes or overdesigned with unused flexibility.
	
	• Test-Driven Development: as we build our stories, we write the test first, and only write production code in response to a failing test. This ensures that every bit of our functionality is covered by test, so that as we adjust the functionality of our system for new stories we know nothing breaks. Such test coverage significantly reduces the need for manual testing, so that our application can grow without the manual testing time increasing indefinitely. TDD also helps us identify and fix design issues in our code that could cause future development slowdown.
	
	• Refactoring: at several different parts of the agile process, we refactor: we change the arrangement of the code without changing its functionality. 
		○  As part of the TDD cycle, we refactor our code as the third step to make it clearer and simpler. When we are looking to add new functionality, we also consider if we can rearrange the code to a new form that better prepares it for adding the new functionality.
		
	• Code Review: as we finish a feature, we push it up to our version control system and open a pull request, which presents the changes for a team member to review. This gives team members a chance to catch bugs and suggest improvements. It also allows them to familiarize themselves with the code so they will not be surprised by it when they need to work on it in the future.
	• Continuous Integration: when a pull request is opened, a Continuous Integration service runs our tests on the branch of code to ensure that our entire suite passes
		○  This means that even if we forget to run the tests ourselves, they will still be run before the PR can be merged. It also ensures the application can run in a new environment, and is not dependent on something implicit in our development environment.
	• Continuous Delivery: agile teams have the ability to release their system at a moment's notice at any time. This includes ensuring that the main source control branch is never broken and doesn't include incomplete work. It also means that the steps to release are automated. 
		○  This doesn't mean that the team necessarily does release to production every time a new feature is completed, but they have the means to do so.
	• Abstractions: agile teams are more interested in delivering business value than custom designing every piece of their application. They use abstractions and shared libraries when they meet the app's needs rather than rewriting them unnecessarily.
		○ The abstractions they reach for might include community standard build setups, UI libraries, full-stack backend frameworks, and hosting solutions like Netlify and Heroku. When the team finds that an abstraction doesn't meet their needs, then and only then do they write lower-level code themselves.


##  Agile Team Practices
	
  
      • Eliciting needs and feedback from business users
      • Coming up with and organizing stories
      • Whether and how to estimate stories
      • Velocity or other measures of the effectiveness of their process
      • Who is part of the team and how their roles work
      • Coordinating design, frontend, and backend work for the same user-facing functionality


##  Testing Concepts


    § Assertions and Expectations
      ○ Asserting: checking that something that should be the case really is the case. A lot of test frameworks have one or more assert() functions that do just that. 


    § Unit Tests
      ○ The term "unit test" refers to an automated test of a portion, or unit, of your code. The difference in use of the term involves what can constitute a "unit".
      ○ The strictest definition of a "unit" is a single function, object, or class. For any dependencies that unit has, they will be replaced by a test double instead of using the real dependencies.
      ○ A "unit" might be allowed to interact with the framework or library it's based on, but still isolated from any application dependencies. Any test that renders a React or Vue component is dependent on React or Vue respectively, but it can still be isolated from data store dependencies and even from child components.

    § End-to-End Tests
      ○ The tests we're referring to here generally simulate a user interacting with your application. There are a number of different names for this type of test that have similar but not quite identical meanings.
      ○ The terms "browser automation tests" and "UI automation tests" focus on the mechanics of the test: that it is automating UI interactions. These terms are broader than just the kinds of tests developers write while building the application functionality: they can also refer to tests QA engineers write to run after the functionality is delivered.
      ○ The terms "acceptance tests", "feature tests", and "functional tests" refer to tests in this category that cover a single feature, a user-facing bit of functionality. These tests are written in terms a user could understand, so that once it passes the user could accept the feature as working. Interestingly, these types of tests are not always written to operate at the UI level; a feature can also be tested by making requests directly to your business logic code. 
      ○ The terms "end-to-end tests" and "system tests" refer to testing an entire system together, not just part of it. 

    § Stubbing and Mocking
      ○ The terms "stubbing" and "mocking" refer to replacing real production dependencies with simpler dependencies that makes testing easier. These terms can be used at both the unit and end-to-end testing level.
        § A stub function is one that returns hard-coded data that satisfies the current test. 
        For example, in one test you might stub a web service call function to return a promise that resolves, and in another test you would stub that function to return a promise that rejects.

        § A mock function is one that allows you to make assertions on whether and how it was called. For example, you might have a form component that calls a passed-in function prop when it is submitted. In the test you would pass in a mock function for that prop, then after submitting the form, check that the function was called with the correct arguments. 
			
			
##    Test-Driven Development


A rapid cycle of forming hypothesis and testing them, a tool for continually validating hypothesis 
	The practice of writing a test for functionality before you write the functionality itself.
		v  It follows a three-step process, "Red-Green-Refactor":
			1. Red: write a test for functionality that does not yet exist, and watch it fail
			2. Green: write only enough production code to pass the test
			3. Refactor: rearrange the test and production code to improve it without changing its functionality
			
![image](https://user-images.githubusercontent.com/44810632/112181583-3cefb680-8c05-11eb-9f2b-0156c34eb6c2.png)

				


##  Why Test-Driven Development?


	• Regression Safety
		Ø As you add new features to your application and change existing features, you need a way to make sure you don't change any functionality except what you intend. Manual retesting becomes impractical as the application grows larger and larger, so an automated test suite is needed. Most developers write tests after the corresponding production code is complete, but this "test-after development" approach has several downsides.
		Ø Test-driven development results in a test suite that fully protects your application's functionality from regressions. It results in 100% test coverage by definition: every line of code you have is the result of a failing test that drove you to write that line. Because of this, you can be sure that if you make an unintentional change it will be caught by the tests. Also, each of your tests adds value: it was required to get some bit of functionality added (or, much less frequently, to cover an important case that was already working correctly). There is no situation where you have code that can't be tested, because the test is what resulted in that code being written
	• Robust Tests
		Ø When a test needs to change any time its production code changes, this is a sign of an over-specified test. The test is specifying details of the implementation of the production code. Instead, what we want is a test of the interface or contract of the production code. Given a certain set of inputs, what are the outputs and effects visible to the rest of the application? We don't care about what's happening inside the module as long as what's happening outside of it stays consistent. 
		
		Ø Testing the contract is what allows you to make production changes without updating your test code: it allows you to make changes to the implementation that don't affect the contract.
		
		Ø Testing the contract is what allows you to make production changes without updating your test code: it allows you to make changes to the implementation that don't affect the contract.
	• Speed of Development
		Ø One way test-driven development speeds up your development is by guiding you to the simplest implementation.
		Ø Test-driven development also guides you to write the simplest interface for a module. 
		Ø With test-driven development, because you have a regression test suite you know you can trust, you can clean up the code any time with very little friction.
	


##  When Not TDD?
	
  
		§ Throwaway code: there is no need for reliability or evolving your code because it will be tried and discarded. If you know for sure the code won't be used on an ongoing basis, this is fine.
		§ Rapidly-changing organizations: for example, in a startup that is pivoting frequently. In systems built for such a startup, you may still want some end-to-end tests that provide stability. But internal code will be more likely to be replaced than evolved, so thoroughly testing it to prepare for changes is wasted effort.
		§ Systems that won't change: the system isn't something that is going to be evolving much over time, because the needs are well understood. It's a system with a known end state. Once that state is reached, further changes will be minimal. 
		§ Spikes: You have a feature you want to implement but you don't know how you want it to work. You want to play around with different alternatives to see how they work before you commit to one. In this approach, you don't know what to specify in a test, and if you did specify something it would likely be thrown out 15 minutes later. 


## Cypress:

    Is a reliable tool to test anything that runs in browser, it shines with testing for modern web apps, like apps built in React, Vue, ..etc.

    Goal is to create an enjoyable testing experience! 




describe(name, fn) groups together several related tests. It takes two arguments: the name of the test block and a function that contains individual tests created using the it() method.


it(name, fn) method contains an individual test. it() takes the name of the test as an argument and a function that contains the test.


Cypress also borrows a set of other methods from Mocha which are called hooks: before(), after(), beforeEach() and afterEach(). The purpose of hooks is to run a function before or after running tests in the file.


test assertions and how they are used in testing.
In simple terms, test assertions are used to verify that the actual result is the same as the expected result. An assertion is passed correctly if the actual result matches the expected outcome, and it fails if these two results do not match.


###    Start with Cypress:
`Yarn add cypress
Npx cypress open`

Created a folder names cypress with example files and test cases to use for a start:


####  Fixtures folder:


Is where you can add the data to mimic or mock the data from an api

![image](https://user-images.githubusercontent.com/44810632/112181716-585ac180-8c05-11eb-9e3b-ac03faadb84d.png)


Data below is a similar version of info we might get from a public API call, this way you can test your app without the need or dependency on the external api.
![image](https://user-images.githubusercontent.com/44810632/112181782-64df1a00-8c05-11eb-9702-808c681c9568.png)



####  Integration folder
![image](https://user-images.githubusercontent.com/44810632/112181794-6872a100-8c05-11eb-9f6c-e9cce08cbdd6.png)



Integration folder is the most important one, as this is where we will add our test cases.

We can access the cypress api using the cy.<command>

To test in cypress we follow certain pattern: 

	• Arrange : 
		○ Visit a webpage
		○ Query this page for an element
	• Act:
		○ Interact with that element, e.g.: click.
	• Assert: 
		○ Make an assertion about this content.


![image](https://user-images.githubusercontent.com/44810632/112181845-71fc0900-8c05-11eb-9598-bafa2da0bf0f.png)




Cypress is all about simplicity!
	![image](https://user-images.githubusercontent.com/44810632/112181884-79bbad80-8c05-11eb-9567-60da28620151.png)

	
	
### 	This could be listed in steps as:
	1. Visit the page at /posts/new.
	2. Find the <input> with class post-title.
	3. Type “My First Post” into it.
	4. Find the <input> with class post-body.
	5. Type “Hello, world!” into it.
	6. Find the element containing the text Submit.
	7. Click it.
	8. Grab the browser URL, ensure it includes /posts/my-first-post.
	9. Find the h1 tag, ensure it contains the text “My First Post”.

###   Ref for elements selection:
https://docs.cypress.io/guides/references/best-practices.html#Selecting-Elements



If Cypress is looking for an element in the DOM that does not exist, it will keep looking for it, (by default 4 sec) then if it fails to find it, it will retire the query and the test will never run.
This gives time for you app to fully function and avoid any confusions like:
	• The DOM has not loaded yet.
	• Your framework hasn’t finished bootstrapping.
	• An XHR request hasn’t responded.
	• An animation hasn’t completed.
	• and on and on…



This means you don't need to use await or any conditional retires.
To match the behavior of web applications, Cypress is asynchronous and relies on timeouts to know when to stop waiting on an app to get into the expected state. Timeouts can be configured globally, or on a per-command basis.
You can change or customize the timeout functionality as you need, Ref: 
https://docs.cypress.io/guides/core-concepts/retry-ability.html#Only-the-last-command-is-retried

![image](https://user-images.githubusercontent.com/44810632/112181931-86400600-8c05-11eb-9baf-31187c491be7.png)



####    Querying by Text Content


Another way to locate things – a more human way – is to look them up by their content, by what the user would see on the page. For this, there’s the handy cy.contains() command, for example:

![image](https://user-images.githubusercontent.com/44810632/112181955-8b04ba00-8c05-11eb-954f-d77aec208892.png)

	

##    Assertions


Assertions describe the desired state of your elements, your objects, and your application.
You should think of assertions as guards.
Use your guards to describe what your application should look like, and Cypress will automatically block, wait, and retry until it reaches that state.
Core Concept
With Cypress, you don’t have to assert to have a useful test. Even without assertions, a few lines of Cypress can ensure thousands of lines of code are working properly across the client and server!
This is because many commands have a built in Default Assertion which offer you a high level of guarantee.



Certain commands may have a specific requirement that causes them to immediately fail without retrying: such as cy.request().
Others, such as DOM based commands will automatically retry and wait for their corresponding elements to exist before failing.
Even more - action commands will automatically wait for their element to reach an actionable state before failing.
Most commands give you the flexibility to override or bypass the default ways they can fail, typically by passing a {force: true} option.



####    Core Concept


By adding .should('not.exist') to any DOM command, Cypress will reverse its default assertion and automatically wait until the element does not exist.


Assertions Ref: https://docs.cypress.io/guides/references/assertions.html#Chai


Disable retry
Overriding the timeout to 0 will essentially disable retrying the command, since it will spend 0 milliseconds retrying.

![image](https://user-images.githubusercontent.com/44810632/112181985-935cf500-8c05-11eb-84ff-72c6acfc77b7.png)



To run Cypress without the GUI we use the command:

`Npx cypress run --headless`



![image](https://user-images.githubusercontent.com/44810632/112182006-97891280-8c05-11eb-9107-78c907ee55ca.png)



This will provide us with the test results and time in terminal without opening up the browser.



Plugins folder: allows you to add extra plugins for functionality like auth,..etc.
Support folder: allows you to create custom commands or re-usable code for cypress.



##    Writing Tests:



Like any other testing lib, we write a test suite, using keyword "describe" inside of it a function and list of "it" blocks each one will test a specific action or value.

The cypress API is cy, which is what we use to get elements, visit pages, etc.


![image](https://user-images.githubusercontent.com/44810632/112182037-9ce65d00-8c05-11eb-8bf1-d7fc6ebedf8f.png)



  cy.get()  >> will get the element on the page, for that you use selectors just like in jQuery.

![image](https://user-images.githubusercontent.com/44810632/112182051-9fe14d80-8c05-11eb-95f5-f5085bd591e1.png)


##    Ways to select elements in CY:


![image](https://user-images.githubusercontent.com/44810632/112182074-a40d6b00-8c05-11eb-8bd8-cd6065ad454f.png)



Way 1:  is good only if you actually need test the page for the text content, like a certain title or header, otherwise if you change the text content during development, marketing,.etc the test would fail and you will have to re-write this selector again.



Way 2 : is not good in most cases, classes names will be changes if you are using something like Tailwind CSS or styled components, that will compile class names into random naming to avoid class names collision or styling issues, so this class names will only be available during development and it won't exist in production, thus this test would fail.



Way 3: using the test id attrb, is probably the way to go, any data-* attrb will be ignored by the browser and it has no effect on the HTML doc. So you can use it safely.



Ref on Selecting Elements: https://docs.cypress.io/guides/references/best-practices.html#Selecting-Elements



###   Changing the View Port in Cypress:

Ref: https://docs.cypress.io/api/commands/viewport.html#Syntax


You create a separate test suite for each view port, at the beginning of the test suite you will use the cy.viewport() to set the dimensions you wish to test.


![image](https://user-images.githubusercontent.com/44810632/112182098-aa9be280-8c05-11eb-829b-aa36cad1a54c.png)




Another cool feature would be to use the with the device name, instead of passing it (width, height)
 cy.viewport('iphone-5')



![image](https://user-images.githubusercontent.com/44810632/112182111-ae2f6980-8c05-11eb-9475-e3b0b3cd6b40.png)


##    Full Example: 


![image](https://user-images.githubusercontent.com/44810632/112182132-b091c380-8c05-11eb-9aa6-669e622269c7.png)



You could use something like the cy.log() to add  log messages as "indicators" before a test would run it would appear like this 


![image](https://user-images.githubusercontent.com/44810632/112182146-b4254a80-8c05-11eb-9dc4-503419f6211d.png)




As we said before, and it is mentioned all over the Cypress docs, cypress run code asynchronously, so code does not code immediately, instead it gets queued for execution.

If you want to log a value , only the first way would work , as it handles the promise being returned from cy.url(), printing it directly would result printing to display 'object' with no actual data displayed.


![image](https://user-images.githubusercontent.com/44810632/112182169-b7b8d180-8c05-11eb-9956-778d2390468b.png)



 
Set Token Authorization using local storage in cypress : Cypress Crash Course - Learn full end-2-end testing using Cypress | 2020 Update



Cypress Patterns and Practices published by Cypress.io 




#   Resources:


	• https://docs.cypress.io/guides/overview/why-cypress.html
	• https://www.youtube.com/watch?v=LcGHiFnBh3Y&ab_channel=Cypress.io
	• https://www.youtube.com/watch?v=azcrPFhaY9k&t=1402s&ab_channel=CodingTech
	• Cypress Patterns and Practices
	• https://outsidein.dev/

![image](https://user-images.githubusercontent.com/44810632/112180413-36ad0a80-8c04-11eb-8931-15c4c8950b6b.png)





# opinion-ate


An app for tracking reviews of dishes at different restaurants.


Production: <https://stupefied-newton-95e06b.netlify.app/>

Dependencies are locked with a `yarn.lock` file, so please use `yarn` and not
`npm` for installing them.


This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

### `yarn start`

Runs the app in the development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in the browser.

The page will reload if you make edits.\
You will also see any lint errors in the console.

### `yarn test`

Launches the test runner in the interactive watch mode.\
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `yarn build`

Builds the app for production to the `build` folder.\
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.\
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `yarn eject`

**Note: this is a one-way operation. Once you `eject`, you can’t go back!**

If you aren’t satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you’re on your own.

You don’t have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn’t feel obligated to use this feature. However we understand that this tool wouldn’t be useful if you couldn’t customize it when you are ready for it.
