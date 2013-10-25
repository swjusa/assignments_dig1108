```
1)  http://www.creativebloq.com/design/choose-right-php-framework-12122774
Using a PHP framework may not be the answer to every project. You need to look at your environment and judge how well a PHP framework can fit in. Here are some pros and cons in using frameworks:

Pros

PHP frameworks can be used as a rapid application development method, enabling quick prototypes to be developed.
As each project is based on a similar structure, it allows for a faster development cycle.
Developers can easily jump from project to project without worrying too much about the structure of the code.
Plays well with Agile software development.
The underlying code will change less often, resulting in a more stable site.
Cons

Some frameworks have a steep learning curve.
It can be difficult to find developers with experience of a particular framework.
Not all frameworks are bug free
Hackers can exploit weaknesses in frameworks.
Different frameworks’ interpretations and supporting libraries of the MVC principle can vary.

2) http://codeception.com/docs/01-Introduction
Introduction
The idea behind testing is not new. You can't sleep well if you are not confident that your last commit didn't take down the whole application. Having your application covered with tests gives you more trust in the stability of your application. That's all.

In most cases tests don't guarantee that the application works 100% as it is supposed to. You can't predict all possible scenarios and exceptional situations for complex apps. But you can cover with tests the most important parts of your app and at least be sure they work as predicted.

There are plenty of ways to test your application. The most popular paradigm is Unit Testing. As for web applications, testing the controller, or model in isolation doesn't prove your application is working. To test the behavior of your application as a whole, you should write functional or acceptance tests.

The Codeception testing framework distinguishes these levels of testing. Out of the box you have tools for writing unit, functional, and acceptance tests in a single manner.

Let's review the listed testing paradigms in reverse order.

Acceptance Tests (WebGuy)
How does your client, manager, or tester, or any other non-technical person, know your site is working? She opens the browser, enters the site, clicks on links, fills the forms, and sees the proper pages as a result. She has no idea of the framework, database, web-server, or programming language you are using. If she sees improper behavior, she will create a bug report. Still this person has no idea why the application didn't work as expected.

Acceptance tests can cover standard but complex scenarios from a user perspective. With acceptance tests you can be confident that users, following all defined scenarios, won't get errors.

Codeception provides browser emulation powered by Mink for writing and executing acceptance tests. This can be done with tools like Selenium, but Codeception with Mink is more flexible for such tests.

Please, note that any site can be covered with acceptance tests. Even if you use a very custom CMS or framework.

Sample acceptance test

<?php
$I = new WebGuy($scenario);
$I->amOnPage('/');
$I->click('Sign Up');
$I->submitForm('#signup', array('username' => 'MilesDavis', 'email' => 'miles@davis.com'));
$I->see('Thank you for Signing Up!');
?>
Pros

can be run on any website
can test javascript and ajax requests
can be shown to your clients and managers
the most stable: less affected by changes in source code or technologies.
Cons

fewer checks can lead to false-positive results
the slowest: requires running browser and database repopulation.
yep, they are really slow.
Functional Tests (TestGuy)
Let's say your application is tested by a technically advanced guy. He also opens the browser, enters the site, clicks links and submits forms, but when an error occurs he can report to you the exception that was thrown, or check the database for expected values. This guy already knows some aspects of your application, and by knowing that his tests can cover more technical details.

Functional tests are run without browser emulation. For functional tests you emulate a web request and submit it to your application. It should return to you a response. You can make assertions about the response, and also access the application's internal values.

For functional tests your application should be prepared to be run in test mode. For frameworks like Symfony2, Symfony1, or Zend, it's easy to start an application in test mode.

Codeception provides connectors to several popular PHP frameworks, but you can write your own.

Sample functional test

<?php
$I = new TestGuy($scenario);
$I->amOnPage('/');
$I->click('Sign Up');
$I->submitForm('#signup', array('username' => 'MilesDavis', 'email' => 'miles@davis.com'));
$I->see('Thank you for Signing Up!');
$I->seeEmailSent('miles@davis.com', 'Thank you for registration');
$I->seeInDatabase('users', array('email' => 'miles@davis.com'));
?>
Pros

like acceptance tests, but much faster.
can provide more detailed reports.
you can still show this code to managers and clients.
stable enough: only major code changes, or moving to other framework, can break them.
Cons

javascript and ajax can't be tested.
by emulating the browser you might get more false-positive results.
require a framework.
Unit Tests (CodeGuy)
Only the developer understands how and what is tested here. It can be either unit or integration tests, but they are limited to check one method per test.

The only difference between unit tests and integration tests is that a unit test should be run in total isolation. All other classes or methods should be replaced with stubs.

Codeception is created on top of PHPUnit. If you have experience writing unit tests with PHPUnit you can continue doing so. Codeception has no problem executing standard PHPUnit tests.

But Codeception provides some good tools to make your unit tests simpler and cleaner. Even inexperienced developers should understand what is tested and how. Requirements and code can change rapidly, and unit tests should be updated every time to fit requirements. The better you understand the testing scenario, the faster you can update it for new behavior.

Sample integration test

<?php
// we are testing the public method of User class.
// It requires the user_id and array of parameters.

$I = new CodeGuy($scenario);
$I->testMethod('User.update');
$I->haveStubClass($unit = Stub::make('User'));
$I->dontSeeInDatabase('users', array('id' => 1, 'username' => 'miles'));
$I->executeTestedMethodOn($unit, 1, array('username' => 'miles'));
$I->seeMethodInvoked($unit, 'save');
$I->seeInDatabase('users', array('id' => 1, 'username' => 'miles'));
?>
Pros

fast as hell (well, in the current example, you still need database repopulation).
can cover rarely used features.
can test stability of application core.
you can only be considered a good developer if you write them :)
Cons

doesn't test connections between units.
most unstable: very sensitive to code changes.
Conclusion
Despite the wide popularity of TDD, few PHP developers ever write automatic tests for their applications. The Codeception framework was developed to make the testing actually fun. It allows writing unit, functional, integration, and acceptance tests in one style.

It could be called a BDD framework. All Codeception tests are written in a descriptive manner. Just by looking in the test body you can get a clear understanding of what is being tested and how it is performed. Even complex tests with many assertions are written in a simple PHP DSL.

3) http://en.wikipedia.org/wiki/Unit_testing
The goal of unit testing is to isolate each part of the program and show that the individual parts are correct.[1] A unit test provides a strict, written contract that the piece of code must satisfy. As a result, it affords several benefits.

Find problems early[edit]
Unit tests find problems early in the development cycle.

In test-driven development (TDD), which is frequently used in both Extreme Programming and Scrum, unit tests are created before the code itself is written. When the tests pass, that code is considered complete. The same unit tests are run against that function frequently as the larger code base is developed either as the code is changed or via an automated process with the build. If the unit tests fail, it is considered to be a bug either in the changed code or the tests themselves. The unit tests then allow the location of the fault or failure to be easily traced. Since the unit tests alert the development team of the problem before handing the code off to testers or clients, it is still early in the development process.

Facilitates change[edit]
Unit testing allows the programmer to refactor code at a later date, and make sure the module still works correctly (e.g., in regression testing). The procedure is to write test cases for all functions and methods so that whenever a change causes a fault, it can be quickly identified.

Readily available unit tests make it easy for the programmer to check whether a piece of code is still working properly.

In continuous unit testing environments, through the inherent practice of sustained maintenance, unit tests will continue to accurately reflect the intended use of the executable and code in the face of any change. Depending upon established development practices and unit test coverage, up-to-the-second accuracy can be maintained.

Simplifies integration[edit]
Unit testing may reduce uncertainty in the units themselves and can be used in a bottom-up testing style approach. By testing the parts of a program first and then testing the sum of its parts, integration testing becomes much easier.[citation needed]

An elaborate hierarchy of unit tests does not equal integration testing. Integration with peripheral units should be included in integration tests, but not in unit tests.[citation needed] Integration testing typically still relies heavily on humans testing manually; high-level or global-scope testing can be difficult to automate, such that manual testing often appears faster and cheaper.[citation needed]

Documentation[edit]
Unit testing provides a sort of living documentation of the system. Developers looking to learn what functionality is provided by a unit and how to use it can look at the unit tests to gain a basic understanding of the unit's API.

Unit test cases embody characteristics that are critical to the success of the unit. These characteristics can indicate appropriate/inappropriate use of a unit as well as negative behaviors that are to be trapped by the unit. A unit test case, in and of itself, documents these critical characteristics, although many software development environments do not rely solely upon code to document the product in development.

By contrast, ordinary narrative documentation is more susceptible to drifting from the implementation of the program and will thus become outdated (e.g., design changes, feature creep, relaxed practices in keeping documents up-to-date).

Design[edit]
When software is developed using a test-driven approach, the combination of writing the unit test to specify the interface plus the refactoring activities performed after the test is passing, may take the place of formal design. Each unit test can be seen as a design element specifying classes, methods, and observable behaviour.
Unit testing limitations[edit]

Testing will not catch every error in the program, since it cannot evaluate every execution path in any but the most trivial programs. The same is true for unit testing. Additionally, unit testing by definition only tests the functionality of the units themselves. Therefore, it will not catch integration errors or broader system-level errors (such as functions performed across multiple units, or non-functional test areas such as performance). Unit testing should be done in conjunction with other software testing activities, as they can only show the presence or absence of particular errors; they cannot prove a complete absence of errors. In order to guarantee correct behavior for every execution path and every possible input, and ensure the absence of errors, other techniques are required, namely the application of formal methods to proving that a software component has no unexpected behavior.

Software testing is a combinatorial problem. For example, every boolean decision statement requires at least two tests: one with an outcome of "true" and one with an outcome of "false". As a result, for every line of code written, programmers often need 3 to 5 lines of test code.[4] This obviously takes time and its investment may not be worth the effort. There are also many problems that cannot easily be tested at all – for example those that are nondeterministic or involve multiple threads. In addition, code for a unit test is likely to be at least as buggy as the code it is testing. Fred Brooks in The Mythical Man-Month quotes: never take two chronometers to sea. Always take one or three. Meaning, if two chronometers contradict, how do you know which one is correct?

Another challenge related to writing the unit tests is the difficulty of setting up realistic and useful tests. It is necessary to create relevant initial conditions so the part of the application being tested behaves like part of the complete system. If these initial conditions are not set correctly, the test will not be exercising the code in a realistic context, which diminishes the value and accuracy of unit test results. [5]

To obtain the intended benefits from unit testing, rigorous discipline is needed throughout the software development process. It is essential to keep careful records not only of the tests that have been performed, but also of all changes that have been made to the source code of this or any other unit in the software. Use of a version control system is essential. If a later version of the unit fails a particular test that it had previously passed, the version-control software can provide a list of the source code changes (if any) that have been applied to the unit since that time.

It is also essential to implement a sustainable process for ensuring that test case failures are reviewed daily and addressed immediately.[6] If such a process is not implemented and ingrained into the team's workflow, the application will evolve out of sync with the unit test suite, increasing false positives and reducing the effectiveness of the test suite.

Unit testing embedded system software presents a unique challenge: Since the software is being developed on a different platform than the one it will eventually run on, you cannot readily run a test program in the actual deployment environment, as is possible with desktop programs.[7]
```