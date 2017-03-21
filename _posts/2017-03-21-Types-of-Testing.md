---
layout: post
title: 'Different Types of Testing'
bigimg: /img/path.jpg
published: true
---

Whether you're beginning your testing career or an elite testing veteran, it's important to keep on track of the most common types and terminology, particularly useful for an interview (probably more so than actually on the job).  This post will outline what I deem to be some of the most current ones to date.  Read more…

**Black box testing:**

Black box testing is testing the software when we have no idea of the internal structure, we have no idea what the source code is like or how it really works, we also have no idea or access to the database(s). We look at the software in question from a customers perspective completely, for example a web application we will strictly look at the GUI and use it how a customer or end user will be using it.

**White box testing:**

White box testing is the opposite, testing when we know the internals of the system.  We are aware of the source code and database structures.  Here we can path accordingly and account for more in depth scenarios, here our tests are based on the coverage of the code, branching / pathing and conditions.  White box testing requires more programming capability from the tester than black box, we will ensure to try and cover:

- Statements - Methods etc, ensuring we can hit as much if not all of the methods applicable, ensuring they will work as expected.

- Branches - Ensuring different scenarios to cover if statements for example, we would ensure to have tests to validate both true and false scenarios

- Paths - Testing to ensure we hit every path through the entire system, ensuring we have traversed through all possible paths atleast once. This does encompass some branch testing as well.

Note: Statement coverage tends to only cover the true side, so lets explain this a little better with some examples.

    Variable num1 & num2
    num3 = num1 + num2
    IF num3 > 50
    PRINT - "Success"
    
Given the above scenario, Our Statement coverage would only encompass one test, one where num3 is infact greater than 50 because we only want to hit the true scenario here. num1 = 25, num2 = 26 would execute all statements from this pseudo code.

But we want to cover the false scenario as well, where num3 is infact less than 50.  This is where Branch coverage comes in, we hit both the true & false scenarios.

To conclude from that then, Branch coverage is a lot more powerful than Statement coverage. 100% branch coverage means 100% statement coverage however the reverse is not true, 100% statement coverage does not mean 100% branch coverage.

Path coverage is a bigger scale, perhaps our software has a path of execution that encompasses multiple if statements, here path coverage becomes very effective, we hit through the path covering every possible scenario.

Unit Testing:
Unit testing would in my opinion be created and maintained by developers and automation engineers, a testing framework should also contain unit tests.  During unit testing we are segregating different parts of the system individually, in theory it could be an entire module, however most of the time it would be specific functions/methods.  An example of a unit test would be if I had the following (java)

    public int calculate(int a, int b) { 
        return a*b;
     }
Here we have a simple calculation function in java, it takes two integers and calculates (returning) their value to the caller.  A simple unit test for this would perhaps look something like this:

     @Test
     public void calculateValid() {
         int a = 25;
         int b = 10;
         int expectedR = a * b;
         int actualR = calculate(a,b);
         assertEquals(expectedR, actualR); 
     }
Above is a simple test against the  calculate method, but there is a whole array of potential tests we can write, this is a brief example of what a unit tests may look like and what its purpose is.

Functional Testing:
Functional testing is typically black box testing which is catered towards the functional requirements of a system.  Functional testing does not mean we are testing a specific function for example, but a piece of functionality of the entire system, providing input and examining the outputs.  Typically we can follow some steps regarding functional testing, these are outlined:

- Creating our input data based on the functions spec
- Determining our expected output based on the functions spec
- Executing our test cases
- Comparison of our actual and expected results
- Check the application functions as per the end users needs
- There are many types of functional testing, some (yes some) of these are:

- Unit & Integration testing
- UAT (User Acceptance Testing)
- Usability testing
- Regression testing
- System testing

Note: Some of these terms haven't been covered in my post as of yet, keep reading and we will cover them all ;)

### Integration testing

Integration testing is where we bring multiple pieces together, think for example a simple web application which had different modules.  Unit testing may target them individually but we need Integration testing when we want to bring them both together and ensure that they A) Interact with each other correctly (if applicable) or B) Do not interfere and cause issues with one another unnecessarily.  To give another example, say we have 3 areas of the system

- Logging in
- Messaging
- Messaging archiving

When navigating between these modules, say via various links, we would be conducting integration testing, we are verifying functionality between modules works as intended.  So a test case may be similar to:

**Objective:** Check the interface link between the Login and Messaging module

**Description:** Enter valid login,  Navigate to users Messaging

**Expected Result:** User is redirected successfully to the inbox

Integration testing becomes especially prevalent when testing API's that are pulling data from other/third party sources and displaying it accurately in your application.  For example my application may have a users balance (which is coming from a third party) so we have to call their API in order to retrieveBalanceForUser().  Here we are verifying our system is retrieving and displaying the balance it is receiving from another system successfully.  Integration testing can also be great at identifying any localisation or environment issues.

### User Acceptance Testing
UAT is also known as BETA testing, it is a part of the process (tho not always incorporated) where the product or application is in the hands of the end users to see if it meets their satisfaction levels.  A common example of UAT on a wide scale would be a games company releasing their game in the beta stage for maybe a few thousand individuals.  These people play the game as end users and the developers of the game would get feedback from them in order to improve the product, or a commercial customer may spend time using the product in order to verify its what they need and fit for purpose.

### Usability Testing:
UX is becoming big business and will grow as time goes on.  Usability testing is the act of having some individuals using the application while monitoring their ability to use it.  Are these users making the same mistakes while using the application? are they slow to achieve certain tasks?  Then usability testing can help to identify the weak points and provide vital information in fixing them.  Typically we would assign these users some tasks to carry out, e.g - send a message to a contact in messaging.  It's likely they are new to the system, from this we can monitor their natural pathing around the system to identify struggle-some areas for users.

### Regression Testing:
Regression testing is the act or re-testing the application under test.  For example, we have a stable application in production already, happy paying customers, great!  Now the customer demands a new module built into the system, such as a shopping module.  Now, while nowadays you would typically take an agile approach to the testing of the new shopping module, we also need to be covering the old existing module with tests as well, this is regression testing.  We are making sure new functionality has not impacted older, stable code.  Typically regression testing would be heavily automated where reasonable but it will always require some manual effort as well.  We need to test the old modules to ensure they are working as intended, building tests which will become regression tests for shopping later on, while identifying ways to remove as much manual effort as possible, Automating the application and API's etc.

### System Testing:
System Testing is a blackbox technique which is used to evaluate the full and complete system under test against the requirements initially specified.  The System is tested from an end-to-end perspective.  To break this down into an example, consider a car manufacturing plant.  Hundreds of parts are created, when a part is attached to another part, this is our integration testing.  Once all parts have been combined we are still at the integration stage up until the last part, now what? we are done? no! we need to verify the car as a whole is suitable (meets requirements etc).  The car is simply not built and upon the final piece attached shipped out to the customer, same applies in software testing.

### End-To-End Testing:
While very similar to System Testing, it does slightly differ.  We will be testing the entire system, however we use an environment that mimics the real world / production use.  Typically we would delve deeply into networks and database connectivity at this point.  How does our application function with databases, networks, interfaces and even other applications.

### Sanity Testing:
Sanity testing is used to determine if a version of the software is performing to a high enough standard to accept it to the testing team to induct testing.  For example if the application is failing to allow logging in, breaking on clicks completely, crashing on initial use then the system is not stable enough to carry on thorough testing, it should be assigned to someone in development to correct before the testers will thoroughly test it.

### Performance Testing:
Performance testing has a number of different subsequent sections related to it. Some (yes, again some!) of these are:

- Load Testing: This is the act of simply applying load to a system, for example we want to simulate 1000 users on the system at the same time and record and analyse the output.  Is the system slow? are deadlocks occuring? are things breaking with concurrency?  These are all things to consider.  Great for assessing likely scalability of the current application/databases.
- Stress Testing: Not to be confused with load testing, stress testing we are expecting the system to fail by going above and beyond what we deem acceptable load levels,  we use this to see which parts of our application will fall over first and fail, allowing us to constantly redine these weaker points in the system.Spike Testing also comes under stress testing, however this is when we send short bursts of high activity at the application and analyse the results.
- Soak Testing: This is the act of testing our application over a lengthy period of time, the application may be stable for a day or two and all will seem ok, however by day 4 or 5 we could be experiencing some issues, this is how we resolve them.  This is extremely effective at identifying memory leaks.
- Capacity Testing: This is used to help you identify a scaling strategy, what type of tech will we need to be using in order to grow our product out and cater to more users or data as time goes on.  We can establish if and how much we need for bandwidth, network drives/storage and processor capacity.

### Security/Penetration Testing:
Like performance, security testing has a number of different subsequent sections related to it, in the recent year(s) it has became much more prevalent (potentially due to major hackings costing big companies heavy fines).

 - Vulnerability Scanning: The purpose of this is to look for known security issues via using tools to match conditions to known    threats.  There are many products on the market which offer these capabilities, a common example would be https://www.metasploit.com/ or OWASP at https://www.owasp.org/
