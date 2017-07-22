---
layout: post
published: false
title: 'Quality Assurance: Questions & Answers'
---
## A New Post

Enter text in [Markdown](http://daringfireball.net/projects/markdown/). Use the toolbar above, or click the **?** button for formatting help.

**Who should have an interest or care about Quality?**
Everyone in the company should have an interest in _good_ quality, not just the development or QA team(s).  Right up to the CEO/External Stakeholders, lack of quality can be extremely detrimental to the organisation as a whole, through lost revenue, damaged reputation etc.  A common misconception is QA is the team that are focused on quality, this view is very narrow minded.

**When should QA be involved in the process?**
From day 1, QA is much more than just testing, QA engineers can input massively into the early design stages of a product.  Early documents should be created right at the beginning, environments need configured, test cases & planning need created, there will be plenty for the QA engineers to be involved in while waiting for the first development build.  Once the first build is received the test execution can begin.

**What is Verification & What is Validation**
Verification is when we look at the software and compare it to the requirements extensively, we are asking ourselves - "Have we made the right product", will our customer be happy with it and have we satisfied all the requirements.

Validation is when we look at the software and ask ourselves - "Have we made the product right".  Did we use appropriate tools, do we have adaquate documentation for what we have done, did we document our APIs, did we utilize TDD/BDD effectively, is our product maintainable, scalable? etc.

Verification evaluates the documentation heavily whereas validation is more focused on the product, verification comes before validation.

**What is the difference in Smoke Vs. Sanity Testing**
Smoke & Sanity testing share some similarities, they are both used as a purpose to determine is the build suitable for more thorough testing, however they do have some main differences.  Sanity testing is a very narrow approach and mostly used when a defect is fixed, has the developer applied a certain degree of sanity to the implemented fix,  for example I have a calculator, when entering 10 * 2 I get returned "25".  This is a sanity test **failure**, basic competence has not been applied by the developer.

Smoke testing is more focused on the core functionality of the system, major functionality if you will.  Here we may test the key areas of the system, such as payments, adding customers etc on a build.  If this stuff is broken we will reject the build and not waste time with more thorough testing.  

**What is the difference in Retesting Vs. Regression Testing**
Retesting is heavily involved around defect fix implementations, testing in an around an affected area on a subsequent build to confirm the defect has been successfully fixed and nothing around that area has been newly introduced as a result.

Regression testing is more widespread and is used to ensure that older stable areas of the system remain that way, regression testing is a means to verify that as a result of new features and functionality that we have not introduced new defects in other areas of the system.  For example we may add a new feature in messaging, the ability to send pictures with a message.  Regression testing may occur on A) the entire messaging module as its likely to be compromised as a result of the new development work but we may also want to test other areas of the system, perhaps we know they are integrated and our work could impact the other modules.

Usually a lot of automation is targetted towards regression testing.

**The Bug/Defect life cycle**
Typically when defects are discovered they will recorded in the defect tracking software and start their life as state: New.  From New they can become four different states, Duplicate; Rejected; In-progress; On-Hold.  Duplicate (if another related defect already exists); Rejected (if the developer/PO deem it not a defect); On-Hold (if its out of scope but we may look at it later); In-Progress (if it has been accepted and work to correct is underway);

From In-Progress it can then (once committed) be marked as Committed, once a build has been deployed to the testing environment, the defect can then be marked as Ready-For-Testing.  From this point the tester can retest the defect/impacted areas and deem the defect to be either: Done/Closed (when it has passed QA) or Re-Opened (If the implemented fix, does not fix the issue).

Rejected bugs are at the end of their life if both QA & Developer agree it is not an issue, it could be Re-opened if it is wrongly rejected;
On-hold bugs can be re-evaluated at a later sprint to see if they enter scope and should be fixed;
Duplicate bugs are at the end of their life if both QA & Dev agree it is a duplicate, it could be Re-opened if a mistake is made with the duplication call.

**What is Defect Severity and Defect Priority**
Defect Severity is the impact on the system (or potential impact).  For example checking out of the E-commerce store causes a server error and takes the web server offline, this is a highly severe (and should be a high priority too!).  

Defect Priority is how soon you should aim to fix the defect, if 2 out of 100 users could not add a particular item to their basket, this is relatively low priority.

**High Severity & High Priority:** Core functionality of the system is broken and as a result can interfere with other users of the system, e.g actions can take the web server offline or security flaws leave customers vulnerable.

**High Severity & Low Priority:** Some reporting functionality of the system is not accessible for a particular group of users, there is no workaround but this area of the system is very rarely used.

**High Priority & Low Severity:** The company logo is missing from the webpage, Login page graphics have been moved location or renamed and the code not updated, 404 returned on the images etc.

**Low Priority & Low Severity:** Footer of a page is missing some text, something basic with no real impact on the end user.

**What Issues do QA Engineers face?**
QA Engineers face a range of issues, most jobs do.  Some of the main problems I have encountered are:

**Lackluster Tools:** Company skimps or refuses to invest in adaquate tooling, this could be test case software, hardware, automation tools, time tracking tools etc.  In order to overcome this problem you should create a business case for the tools in question, analysing your need for them and present it to your line manager.

**Lack Of Training:** Work requires learning new skills or the team does not have all bases covered from a skill set perspective, for example how to test APIs.  To overcome this problem you should speak to your line manager alerting them about the defeciency of skills within the team for that area and present some recommendations for training which could help the team, import to document the learning for newer starts later.  

**Application instability:** The application is very unstable, there are a lot of defects and progressing is taking much slower than expected, this could be due to inexperienced developers working on the project, unmaintainable code starting to come back and haunt us.

**Bad Processes In & Out of the QA Department:**  QA Processes are not well defined or are lack luster in some avenues, same goes for outside QA processes, e.g development or business processes which impact on QA.  To overcome this problem you should figure out which processes are A) Missing and begin researching how they can be implemented and B) Alert your line manager who can then bring your thoughts to perhaps the management meeting which could result in the processes being implemented and tweaked/fixed to improve effeciency.

**Lack of Resourcing:**  Estimations without QA input or the company/business promising more than can be comfortably delivered, QA department is squeezed and feels undervalued.  The best way to improve this problem is to parttake in estimations and make your concerns known to management so they can (with your help) begin correcting them.  

**Lack of or ambiguous Requirements:** The customer provide little to no help or unclear requirements, in order to overcome this problem you should try to push forward more story telling sessions and communicate with the customer making them aware that it is in both parties interests to develop clear concise criteria here, define solid entry criteria around this.

**What are the roles of QA?**
QA has a range of different responsibilities, some of the main responsibilities of the QA role are:

-Implement, Maintain & Execute the testing processes
-Observe & advise on the overall development processes
-Offer assistance with issues of the software, we are product experts after all
-Log & Monitor defects through the software life cycle
-Participate in product innovation
-Participate at all stages of the SDLC
-Manage the STLC
-Provide adaquate reporting & communication on the testing process
-Stay up to date on technologies and industry trends
-Estimating the testing effort
-Being part of the company in general, part take in events & social activities etc.

**What is the difference in Build & Release?**
A Build and Release are in essence, the same thing for a small portion of the sprint and by that I mean, the final build for testing, is technically the release.  As sprints progress, the QA team will receive a number of builds, maybe daily, maybe on demand self triggered via commits etc.  In theory these builds become more stable as the sprint progresses and more and more defects get fixed, when the exit criteria is met and management are happy to release, we can version the most stable build and release it to either a customer, beta testing environment or UAT environment.  The release build is versioned accordingly whether that be apps version name, web assembly/dll's etc.

**What is test automation & what criteria is good for automation?**
Test automation is when we identify manual tests which we could see a great return on investment by making them automated through the use of computer code.  Automation occurs at various levels, typically the Unit, Integration & UI.  Good test cases to automated are things which are known to be unreliable & by that I mean areas of the system that fall down repeatedly.  Areas of the system which are relatively simplistic but time consuming to execute for manual testing.  Areas of the system which are known to be stable currently, spending time on something that has a huge overhaul incoming in a few weeks is not a smart use of time or resources.  Something which is critical to the application, common areas that under go smoke testing are a great place to start.  APIs and integration/service level tests should be highly automated as they are relatively lightweight in comparison to selenium end2end GUI tests.

**What is Bug Leakage & What is Bug Release?**
Bug Release is when the build is provided to the QA team or possibly even the end user when we are aware of existing defect(s) in the build, for example due to time constraints we may be forced to release when the release likely includes a few known minor defects.

Bug Leakage is when a defect survives the entire development/QA process and is typically discovered during UAT or in production itself, defects become very expensive the longer they take to discover, exploding in production is very expensive and damaging to the companies reputation.

**What is Data Driven Testing?**
Data Driven testing is when we typically have some sort of DataProvider, for example an excel spread which houses a wide range of various inputs, for example we may have a login on our web application, our Data Drive content would provide a host of different username/password combinations.  We read from this Data source and use it to populate the tests, in automation something like a TestNG @DataProvider would be used for running a DataDriven framework, or using BDD Cucumber something like a Datatable would be used to populate the tests.

**Alpha Vs. Beta Testing?**
Alpha testing typically happens IN HOUSE by the development team and before the QA team receive the builds to test on an environment which mirrors that of the production environment.

Beta testing is when the organisation may use a public or private group of people to test their product before going live with it essentially, very prevalent in the games industry,a closed beta may allow a few thousand select individuals to try out the new features and functionality before it is released to the masses, this helps mature the product towards real users needs, has a big range of people using it to find existing defects, much more than your internal development/QA team would find.

**What is a bug triage?**
A Bug triage is part of the agile process and is used to assess the current defect list, here we evaluate each individual defect firstly for its current state, should something be put on hold for another release? is the severity & priority of the defects accurate.  Is the defect assigned to the appropriate person? we can modify that during the bug triage meeting. 

**What is a Traceability Matrix?**
A Traceability Matrix is used to demonstrate the satisfaction of requirements throughout the testing process.  Requires vs. test cases so to speak, requirements are listed across one axis with test cases on the other, where the test case and the requirement meet on the grid and that case can satisfy to requirement or part of it, it is marked with a **x**.  This way we can easily identify if we are doing work outside of the requirements and possibly out of sceope, but also say with confidence that the requirements have been met and thoroughly tested.

**What makes a good test case?**
A test case should be easily executable for someone who is new to the system, write them to include all necessary information for maintainability later.  Test case should include any assumptions or prerequisites.  Each step should make logical sense, with clear consise actions accompanied with assertable expected criteria.  Perhaps using a BDD approach @Given, @When, @Then.

**What are the benefits of Automated Testing?**
Very instant-relatively instant feedback, very cost effective.  Essential for building scalable, reliable, maintainable products.  Allows the manual effort to focus on more exploratory testing to take a curious view of the system and discover unique defects.  Provides career pathing and advancements for the QA team / department.  Heavily reduces the manual testing efforts, especially when executing regression testing. Automated generated documentation, such as dashboards etc provide instant visual feedback, very useful for providing to non technical folks.  Increased release confidence, improving the testing process effeciency.
A good framework can allow non technical people to add tests after using plain english text.

**What is Agile and what are the benefits?**
Agile is a software development life cycle, typically consisting of a scrum or kanban approach.  The concept is smaller incremental releases with an iterative approach while heavily involving the customer and members from the business side.  Agile typically involves 6 steps -> Requirement Analysis; Design; Creation/Development; Testing; Deployment; Maintainance.  After each sprint there should be appropriate retrospective(s) in order to improve the teams performance for all future sprints.  Each of these steps are repeated over the iteration.

The main benefits of Agile are: The testing is happening much quicker in this system, unlike the older waterfall model testing coming quite late in the overall process where it is too late to back track, this is a much faster response and cost effective system.  Customers are involved heavily in the process of defining the requirements and coupled with mid or end of sprint demos they get a good feel for what we are building, rather than keeping them in the dark and then showing them something they potentially won't like.  Internal work force has more responsibilities within the team, members take on tasks outside of the norm occassionally and develop themselves technically.  Company is building high performing teams that can be moved around on various projects leader creating a more effecient work force.  Less risk in building the wrong software and more emphasis on building the software **right**.

**What types of testing would you perform on web applications?**
Web applications will undergo a range of different types of testing, non functional aspects like testing the application for security, performance, usability and accessibility.  Web applications will also have unit & integration tests automatically executed.  Functional testing types are also performanced, such as Regression, Smoke/Sanity, System & End2End testing are utilised.







