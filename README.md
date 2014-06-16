Sel_learn
=========
Now, consider the Test scenario Check Login Functionality there many possible cases like  Check response on entering valid Agent Name & Password ,Check response on entering invalid Agent Name & Password ,Check response when Agent Name is Empty & Login Button is pressed, and many more
This is nothing but Test Case. Test scenarios are rather vague and cover a wide range of possibilities.  Testing is all about being very specific.Hence we need Test Cases
Now just Consider the test case , Check response on entering valid Agent Name and password. Its obvious that this test case needs input values viz.Agent Name & Password
This is nothing but Test Data. Identifying test data can be time-consuming and may some times require creating test data afresh. The reason it needs to be documented
Before we proceed ahead  consider a quote from a witty man who said "To ensure perfect aim, shoot first and call whatever you hit the target" But if you do not live by this philosophy ,which I am sure most of you do not then your Test case must have an expected result.
For our test case, expected result would be , Login should be successful
If expected results are not documented we may miss out on small differences in calculations in results which otherwise look OK.
Consider this example, where you are calculating monthly pay for an employee which involves lots of calculations. The need for documenting expected results becomes obvious.
Suppose the author of the test case  has left the organization or is on a vacation or is sick and off duty or is very busy with other critical tasks and you are recently hired and have been asked to execute the test case.Since you are new, it would certainly help to have test steps documented which in this case would be Launch application , Enter Agent Name,  Enter Password , Click OK
You may wonder that for this simple test steps, documentation is not required
But what is your test steps looked something like this ? (pic in video) I think the need will becomes instantaneously obvious.
That apart your test case -may have field  like  , Pre - Condition which specifies things that must in place before the test can run
For our test case , a pre-condition would be Flight Reservation Application should be installed , which I am sure 50% of the people watching this tutorial do not have
Also, your test case may also include Post - Conditions which specifies anything that applies after the test  case completes.
For our test case , a post - condition would be  time & date of login is stored in the database
During test case execution , you will document the results observed in the Actual Results column and may even attach some screen shots and based on the results give PASS & FAIL status.
This entire table may be created in Word , Excel or any other Test management tool.That's all to Test Case Design
Testing Techniques
It's not possible to check every possible condition in your software application. Testing techniques help you select a few test cases with the maximum possibility of finding a defect.

 Boundary Value Analysis (BVA): As the name suggests it's the technique that defines the testing of boundaries for specified range of values.

 Equivalence Partition (EP) :This technique partitions the range into equal parts/groups that tend to have same behavior.

 State Transition Technique: This  method is used when software behavior changes from one state to another following particular action.

 Error Guessing Technique: This is guessing/anticipating the error that may arise while testing.This is not a formal method and takes advantages of a tester's experience with the application

Test Management Tools
Test management tools are the automation tools that help to manage and maintain the Test Cases. Main Features that tools opted for are:

For documenting Test Cases: With tools you can expedite  Test Case creation with use of templates

Execute the Test Case and Record the results: Test Case can be executed through the tools and results obtained can be easily recorded.

Automate the Defect Tracking:Failed tests are automatically  linked to the bug tracker  , which in  turn can be assigned to the developers and can be tracked by email notifications.

Traceability :Requirements, Test cases, Execution of Test cases are all interlinked through the tools and each case can be traced against each other to check test coverage.

Popular Test Management tools are : Quality Center  and  JIRA

  Guidelines/Best Practice/Tips for writing test cases.

1. Test Cases need to be simple and transparent:

Create test cases which are as simple as possible. They must be clear and concise as author of test case may not execute them.

Use assertive language like go to home page, enter data, click on this and so on. This makes the understanding the test steps easy and test execution faster.

2. Create Test Case with End User in mind

Ultimate goal of any software project is to create test cases that meets customer requirements and is easy to use and operate. A tester must create test cases keeping in mind the end user perspective

3. Avoid test case repetition.

Do not repeat test cases. If a test case is needed for executing some other test case , call the test case by its test case id in the pre-condition column

4. Do not Assume

Do not assume functionality and features of your software application while preparing test case. Stick to the Specification Documents.

5.  Ensure 100% Coverage

Make sure you write test cases to check all software requirements mentioned in the specification document. Use Traceability Matrix to ensure no functions/conditions is left untested.

6. Test Cases must be identifiable.

Name the test case ids such that they are identified easily while tracking defects or identifying a software requirement at a later stage.

7. Implement Testing Techniques
Testing techniques must be used for effective testing.

Suppose you encounter a scenario to test a good deal of values. In such a case apply both Boundary Value Analysis and Equivalence Partitioning techniques. This will aid in covering a good range of value and avoid unnoticed defects.

In case Application has many pages/integrations then create test cases for each State Change by implementing the State Transition Technique.  

8. Peer Review.

After creating test cases, get them reviewed by your colleagues. Your peers can uncover defects in your test case design, that you may easily miss. 

Resources

Download -Sample Test Case Specifications Template for your reference. Please note that the template used will vary from project to project. The below zip file contains three popular templates used in the industry.
Bassics of slenium
