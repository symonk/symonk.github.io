---
layout: post
title: 'Different Types of Testing'
bigimg: /img/path.jpg
published: true
---

The aim of this blog post is to attempt to encapsulate some of the commonly known terminology around testing into one easy to read (and interpret!) place.  Terminology comes and goes and new types of testing, processes and methodologies enter the space on a daily basis.  We will start the blog post off with something that most of the readers will be familiar with, Black Box Testing & White Box Testing.  Simply put, Black Box Testing is when we assume the role of an end user, functionally using the system.  We have no idea of any of the inner workings, we do not know what the source code looks like, we do not know anything about database structure, queries or stored procedures etc.  We load up the system, we login and we replicate end user actions and investigate based solely on things available to us.

White Box Testing Vs. Black Box Testing

White Box Testing is slightly more intrusive, we may be aware of the database structure, what queries and stored procedures are firing off as a result of our action(s) and can freely access the source code.  We can debug and step through the code to really investigate what is going on, we can access the database to check out data/table structure, where and when data is moving and any stored procedures that could be getting called.

The big question then, which is better?  The answer is neither, if you are not applying both of these testing techniques you are severely holding yourself back in terms of what you will find and how you develop as a engineer in this space.  Both are essential in creating quality software, however White Box Testing will without a doubt advance your technical skills, help you nail those really rare hard to find defects and build a solid career for yourself in the mean time.

Lets say we are working at a company which has a relatively complex windows service, when an Android tablet is connected to service begins to flow from start to finish, sending thousands of commands to your device based on a wealth of scenarios, this can seem daunting at first but with good White Box Testing techniques, we can build out our testing strategy to strengthen our service and advance our product.  How do you do this then? using some White Box Testing techniques that I will outline below:

Statement coverage: Statement coverage is the act of hitting atleast all of the statements in our code at least once, typically statement coverage will opt for the true option as conditional statements typically ask for if/when something is true, do X, the main draw back being, we aren't evaluating the false scenario(s).  Consider the below example:

Pseudo Code Example:
    Variable num1 & num2
    num3 = num1 + num2
    IF num3 > 50
    PRINT - "Success"

Looking at the above code, our statement coverage would just ensure the sum of num1 + num2 was greater than 50.  Why? Because we have successfully executed the true scenario here which results in "Success" being printed.  As Mentioned earlier, we are ignoring the scenario here that num3 is less than or equal to 50.

Branch coverage: Branch coverage is similar to Statement Coverage, however we also want to encompass the false scenarios here.  Lets consider another piece of pseudo code, an IF/ELSE Statement,  see our psuedo code below:


    Pseudo Code Example:
    Variable number
    IF (number > 10)
    PRINT - "Hi"
    ELSE
    PRINT - "Bye"



With Statement coverage, we would just set "number" to something over 10, but using Branch Coverage we want to hit the ELSE condition here also, so we would essentially have two scenarios, where number = less than or equal to 10 & where number = greater than 10.  With these two scenarios, all lines of the above pseudo code would see execution.

Branch coverage is a lot more powerful that statement coverage and yields much better results.  Branch coverage achieves Statement coverage, but we cannot assume the reverse, Statement coverage covers little of Branch coverage.

Path Coverage: Path coverage is the most complex white box testing technique, here we are assessing the flow throughout our software, our aim is simple - cover all lines of code & scenarios throughout.  This can get complex and we need to factor in our IF, UNTIL & WHEN Constructs.  Mapping out control flow diagrams can be extremely useful here,  a basic example of path coverage is outlined below:


So, looking at our diagram, Statement Coverage = 1, Branch Coverage = 2, Path Coverage = 4, Why? Simple - we need to hit the following paths to successfully execute our system from start to finish:

1A-2B-E-4F
1A-2B-E-4G-5H
1A-2C-3D-E-4G-5H
1A-2C-3D-E-4F

Unit Testing

 This is a term you will come across often and something many developer(s) or companies either A) Dislike doing or B) Don't know to do, it does  take a little time so whats  the point wasting time, lets make millions instead!  Unit testing has vast benefits for software but before we begin don't neglect unit testing within the automation framework itself, this is something that is really popular, unit test your test framework!  Thing of a unit test as some code with the sole purpose of testing live/production bound code.    What is the benefits? When you eventually build your product bigger and bigger, lack or no unit testing will hit you hard, making even the smallest changes startes creating a massive unknown, what is broken as a result? we haven't got a clue! it's OK, QA will spot it!  Unit testing/TDD helps you know when its time to stop coding, this is more and more important with the hip new agile way everyone is crazing about.  Some big advantages of unit testing are:

As previously mentioned, it contributes later to quickly releasing code changes in a stable manner, retaining software quality
You will be surprised at how what seems to be daunting situations to overcome can be easily digested by unit testing/TDD in general.
Invaluable instant/almost-instant feedback
Catching issues earlier in the development cycle, forget making millions, lets save millions!
Makes you feel good (person-specific, no promises).
Imperfect tests executed often are much better than perfect tests never executed
I could go on all day but lets be fair for anyone reading who doesn't see the advantages here is a disadvantage, it does take a little time. As everything is a bit easier to digest with an example, see the below example for calculating the sum of two ints:

public int calculate(int a, int b) { 
    return a*b;
 }

In order to unit test this, we could begin with the following unit test:

@Test
 public void calculateValid() {
     int a = 25;
     int b = 10;
     int expectedR = a * b;
     int actualR = calculate(a,b);
     assertEquals(expectedR, actualR); 
 }
This is an extremely simple example, but you get the concept we are writing test code to invoke and evaluate our production code with typical Expected and Actual results.

Functional Vs Non Functional

These are two other terms that are thrown about often and I will be writing another post dedicated to these specifically, so please check back later, as of now they are currently in writing, but if you can't wait (I know you couldn't) here is a simple overview of Functional testing.

Functional Testing: Functional testing is typically black box testing which is catered towards the functional requirements of a system. Functional testing does not mean we are testing a specific function for example, but a piece of functionality of the entire system, providing input and examining the outputs. Typically we can follow some steps regarding functional testing, these are outlined:

Creating our input data based on the functions spec
Determining our expected output based on the functions spec
Executing our test cases
Comparison of our actual and expected results
Check the application functions as per the end users needs
My article on Functional Vs Non Functional can he found here: http://www.editmelater.com

Sanity Testing

Sanity testing (not to be confused with insanity - thats something completely different) is performed after a build has been deployed but before regression or functional testing occurs, note we deem it Sanity testing with minor changes have been committed to the build to ensure sane rational has been applied by the developer before we commit to properly testing it, for example if we had a calculation on our web app that was recently changed and if we initially input 2 * 2 with a result of 10, this build has failed and we will not be wasting any time on it.

Smoke Testing

Smoke testing is very similar to sanity testing, however we are assessing what we deem core functionality here, the purpose is to deflect any badly broken builds from getting a dedicated testing effort.  For example core functionality of the application would be checked quickly, adding a new product etc, upon failure of the core functionality the build has failed and we will not be wasting any on it.  It is very effective to script or automate the smoke testing as it encompasses fundamental areas or key functioning areas of the system.  It is also important to execute smoke testing on production deployments to verify the installation has been successful.

Integration Testing

Integration as the name suggests is the act of testing out different components interact with each other, because a particular module in a system doesn't directly interact with another, with a modern movement towards modularisation and microservices managing the integration of components is vastly improving.  Integration can be a particular painpoint for a number of reasons, what may seem like it is not linked at all at the front end can be messy in the backend, typically different teams or individuals may work on seperate modules and their interpretation or way of doing something could clash with anothers.  With integration we are essentially accessing the flow of data or information or user interaction(s) between our modules.  Lets take a simple scenario, we have a messaging module in the system and a reporting module, the aim when testing this is that we can use the messaging module as normal but when we want to access reporting we are able to do so and the information necessary for messaging reporting is accessible to generate the appropriate tests.  Sending a bunch of messages and then generating a report on those messages is an example of integration testing between those two modules.  Even the ability to navigate between these modules as a user is to some degree, integration.  A great example of integration testing is how your software is interacting with third party API's, for example you may have a page on your website taking a users address and presenting it via google maps, this is integration testing between googles maps API and your software.  It is quite common for exception handling to be noticeably weaker around points of integration.


User Acceptance  Testing

UAT is also known as BETA testing, it is a part of the process (tho not always incorporated) where the product or application is in the hands of the end users to see if it meets their satisfaction levels. A common example of UAT on a wide scale would be a games company releasing their game in the beta stage for maybe a few thousand individuals. These people play the game as end users and the developers of the game would get feedback from them in order to improve the product, or a commercial customer may spend time using the product in order to verify its what they need and fit for purpose.

Regression Testing

Regression testing is the act or re-testing the application under test. For example, we have a stable application in production already, happy paying customers, great! Now the customer demands a new module built into the system, such as a shopping module. Now, while nowadays you would typically take an agile approach to the testing of the new shopping module, we also need to be covering the old existing module with tests as well, this is regression testing. We are making sure new functionality has not impacted older, stable code. Typically regression testing would be heavily automated where reasonable but it will always require some manual effort as well. We need to test the old modules to ensure they are working as intended, building tests which will become regression tests for shopping later on, while identifying ways to remove as much manual effort as possible, Automating the application and API’s etc.

Usability Testing

UX is becoming big business and will grow as time goes on. Usability testing is the act of having some individuals using the application while monitoring their ability to use it. Are these users making the same mistakes while using the application? are they slow to achieve certain tasks? Then usability testing can help to identify the weak points and provide vital information in fixing them. Typically we would assign these users some tasks to carry out, e.g - send a message to a contact in messaging. It’s likely they are new to the system, from this we can monitor their natural pathing around the system to identify struggle-some areas for users.

System Testing

System Testing is a blackbox technique which is used to evaluate the full and complete system under test against the requirements initially specified. The System is tested from an end-to-end perspective. To break this down into an example, consider a car manufacturing plant. Hundreds of parts are created, when a part is attached to another part, this is our integration testing. Once all parts have been combined we are still at the integration stage up until the last part, now what? we are done? no! we need to verify the car as a whole is suitable (meets requirements etc). The car is simply not built and upon the final piece attached shipped out to the customer, same applies in software testing.

End to End Testing

End-to-end testing involves ensuring that the integrated components of an application function as expected. The entire application is tested in a real-world scenario such as communicating with the database, network, hardware and other applications.

For example, a simplified end-to-end testing of an email application might involve:

Logging in to the application
Accessing the inbox
Opening and closing the mailbox
Composing, forwarding or replying to email
Checking the sent items
Logging out of the application
Performance Testing

Performance testing is quite a big space, it can be broken down into multiple subsections,

Load Testing

This is the act of simply applying load to a system, for example we want to simulate 1000 users on the system at the same time and record and analyse the output. Is the system slow? are deadlocks occuring? are things breaking with concurrency? These are all things to consider. Great for assessing likely scalability of the current application/databases.

Stress Testing

Not to be confused with load testing, stress testing we are expecting the system to fail by going above and beyond what we deem acceptable load levels, we use this to see which parts of our application will fall over first and fail, allowing us to constantly redine these weaker points in the system.Spike Testing also comes under stress testing, however this is when we send short bursts of high activity at the application and analyse the results.

Recovery Testing


Recovery testing is where we purposely stress test our application to breaking point and analyse how long if at all it takes to recover.

Soak Testing

This is the act of testing our application over a lengthy period of time, the application may be stable for a day or two and all will seem ok, however by day 4 or 5 we could be experiencing some issues, this is how we resolve them. This is extremely effective at identifying memory leaks.

Capacity Testing

This is used to help you identify a scaling strategy, what type of tech will we need to be using in order to grow our product out and cater to more users or data as time goes on. We can establish if and how much we need for bandwidth, network drives/storage and processor capacity.

99% of the time we use Performance testing as a means to identify the following - are database queries & stored procedures optimised?, is the application only invoking these when necessary?, are we receiving deadlocks in production? Are Page, API, Database calls slow or stalling and erroneous? Is our application or certain aspects of it using weird bandwidth, memory, CPU or disk I/O levels?  Are response times getting out of control under bigger loads?

You would be very surprised the performance a badly designed system can suffer when it is used by many concurrent users, in order to start getting a handle on this stuff, check out my entry level Jmeter tutorial here: https://www.symonk.github.io/2017-02-23-Jmeter-POST-Login/

An absolutely invaluable  tool can be found here: https://www.appdynamics.co.uk/, I use this tool to monitor production and it provides a wealth of information to me for all layers of the system.

Security & Penetration Testing

Just like Performance, the Security sector can be broken down into many different subsections and if you are starting out in security / penetration I urge you to get familiar with the OWASP TOP 10, this is a list of the most common area in which web applications fall down to malicious attack vectors.

Vulnerability scanners

The purpose of this is to look for known security issues via using tools to match conditions to known threats. There are many products on the market which offer these capabilities, a common example would be OWASP ZAP at https://www.owasp.org/ or BurpeSuite https://portswigger.net/burp/.  Metasploit from Rapid7 is also an amazing piece of software for exploring and using known exploits, a must for any upcoming pentester.

SQL Injection

In the simplest form, SQL Injection is when an attacker can pass in strings that are added into your queries and executed as code, consider the following field,  customerID=12.  In our backend code (rarely nowadays, but still happens) the we may be interpreting the ID and passing it into a SQL query, for example:

SELECT * FROM myTable WHERE customerID = '12', in order to exploit us, a hacker may attempt to pass in customerID=12 105 OR 1=1 to reveal information that is not intended.  This is a simple form of a SQL Injection attack and when used can compromise your entire database and data associated with it.  Various other attacks of similar nature are also in existence, e.g LDAP, OS, XXE Injection

Broken Session Management & Validation

This is typically when an attacker can steal or easily retrieve accounts via unprotected user credentials, sessionID's, weak or non existent password strengthening.  Things like infinite (non expiring) sessionIDs can be easily manipulated or are based on some weak algorithm, e.g incrementing each time - this allows a hacker to predict a valid session and just wait for the victim to be assigned it.  Using HTTP is a disaster, network sniffing will easily identify your username/passwords and sessionID / cookies.  Sadly some software companies will choose to enforce their login using HTTPS and then redirect to HTTP once logged in, to a naive eye this seems like an OK solution, if someone is sniffing our users at login they will get a face full of encrypted credentials, excellent! - What happens when redirected to HTTP and send any sort of HTTP request? its likely their cookies and sessionID are then sent to the server in plaintext, intercepted and session duped for a successful login for the attacker.

Cross Site Scripting

This one is pretty interesting and I like to think of it in two forms, Reflective and Persistent.  We will start with persistent, this is the most dangerous XSS method because its somewhere in your database being delivered to everyone of your users/victims. Consider a comment form on a blog post, a hacker attempts to POST their data via the GUI containing malicious javascript, due to bad security its successfully landed in your database, now on page load of the comments the script is going to be ran on every users browser who opens the page, absolute disaster.  Typically a hacker would setup their own server and send the users cookies & other information to their server to steal it, however it is possible to phish & keylog a user by running client-side javascript, for more on this check out BeeF on Kali Linux, pretty amazing what is possible when a javascript hook on the victims browser.

Second is reflective XSS and this typically requires a bit of social engineering and tricking the victim on the hackers part, for example if your website has a search function which amends a URL ?search=abc, if vulnerable to XSS an attacker can craft a URL of your website to send on to unsuspecting victims, when they click the link the XSS is executed in the clients browser, there is much less chance of wide spread problems with this method, however having either as options on your website or application is a disaster.

Broken Access Control

This one is pretty self explanatory, for example accessing hidden pages via just passing in the full URL, errors in user account / role accessibility or complete lack of any sort of validation against user privs/permissions can cause all sorts of problems in your application.

Security Misconfigurations

A lot of people neglect all angles of attack, if your web application is absolutely bulletproof (sorry to tell you, it isn't!)  Is your network bulletproof? is your database bulletproof?  Using default accounts e.g "sa" on Microsoft SQL Server are a big no no, using accounts with privileges and access more than necessary is a huge no no, the most excessive rights services and accounts have, the more possible damage can be done if they are compromised.  Are your servers up to date? if you servers are lacking windows updates they will be vulnerable exploits, have you badly setup some software ? NMAP scanning combined with Metasploit could make your network and or application(s) a complete lottery for hackers.  Next up is error & exception handling, are you revealing sensitive information such as a stack trace? if so you better stop it, anything you give is making it easier for attackers, is your tech setup correctly and securely? even if you are using things like SpringMVC and very popular frameworks / libraries you need to ensure appropriate settings are configured to remain secure.

Sensitive Data Exposure

Sensitive Data Exposure is pretty straight forward, the elephant in the room is - are you transferring sensitive data unencrypted / in plain text and secondly are you storing it that way, everyone focuses on the storing of the data and often neglects the initial transfer of it.  If encrypted are you using suitable encryption levels? e.g Using MD5 stuff nowadays is suicide, is your SALT the same for every user? typically you want it completely randomised per user per transaction.  Are your HTTP responses/ headers adaquately setup.  Are your systems safely validated? for example, consider this page profile?id=100, this displays my profile, but what if i manually change it to id=101, am I shown someone elses information?

Insufficient Attack Protection

Consider anyone with network access can send your application a request. Does your application detect and respond to both manual and automated attacks?

Detecting, responding to, and blocking attacks makes applications dramatically harder to exploit yet almost no applications or APIs have such protection. Critical vulnerabilities in both custom code and components are also discovered all the time, yet organisations frequently take weeks or even months to roll out new defenses.

It should be very obvious if attack detection and response isn’t in place. Simply try manual attacks or run a scanner against the application. The application or API should identify the attacks, block any viable attacks, and provide details on the attacker and characteristics of the attack. If you can’t quickly roll out virtual and/or actual patches when a critical vulnerability is discovered, you are left exposed to attack.

Do you have adaquate systems in place to prevent brute forcing attacks? Does your system impact user experience? if so you need to rethink your defence, things like displaying usernames (username enumeration) are also terribly bad and allow hackers to harvest your data for more potent attacks later.

Cross Site Request Forgery [CSRF]

Cross Site Request Forgery is another interesting one, consider a banking system where a logged in user can send balance using a GET request (terrible, I know.. but you get the point).  ?transferFundsAmount=500&transferToAccount=ref500.  This HTTP GET request will transfer $500 to the account "ref500".  What CSRF basically does is when a user is authenticated on the bank for example, a hacker can craft a request and force the user into navigating to it in order to slyly execute the bank transaction in the background, this can be done with an image attachment for example where the <img src> contains the request.

To check whether an application is vulnerable, see if any links and forms lack an unpredictable CSRF token. Without such a token, attackers can forge malicious requests. An alternate defense is to require the user to prove they intended to submit the request, such as through reauthentication.

Using Components with known vulnerabilities

Like previously mentioned, exploits are found daily e.g NSA leaks from ShadowBroker releasing various tools and zero days, one of which was incorporated into the recently widespread WannaCrypt.  Using outdated or known vulnerability components at any level will eventually end in disaster.  Make sure everything you use is A) Actively maintained, B) has suitable defences in place and C) is Updated often.  Keeping an active eye on exploit databases online can be extremely helpful too, but most great exploits when discovered are not released or detected for a very long time, it is not profitable for those who discovered them to turn them over, good zero days are worth well into 6 figures on the black market.

What is a zero day? -  zero-day (also known as zero-hour or 0-day) vulnerability, It is known as a "zero-day" because it is not publicly reported or announced before becoming active, leaving the software's author with zero days in which to create patches or advise workarounds to mitigate its actions.

Unprotected API's

Testing your APIs for vulnerabilities should be similar to testing the rest of your application for vulnerabilities. All the different types of injection, authentication, access control, encryption, configuration, and other issues can exist in APIs just as in a traditional application.  

Imagine a public API offered by an Internet startup for automatically sending text messages. The API accepts JSON messages that contain a “transactionid” field. The API parses out this “transactionid” value as a string and concatenates it into a SQL query, without escaping or parameterizing it. As you can see the API is just as susceptible to SQL injection as any other type of application.

Imagine a mobile banking app that connects to an XML API at the bank for account information and performing transactions. The attacker reverse engineers the app and discovers that the user account number is passed as part of the authentication request to the server along with the username and password. The attacker sends legitimate credentials, but another user’s account number, gaining full access to the other user’s account.

Trusting Client side Validation

This is one of the most common pitfalls, sticking some validation on a textbox and throwing everything else out the window, its ok the user can only enter 5 numeric characters in that textbox! No, client side validation is weak, the request can easily be manipulated and the request can contain data you were not expecting, will your server respond well and hold up in this instance? I'm going to guess you haven't even thought about it.  How does your server hold up when the int it was expecting is a 60 character string, let us know.
