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

**Bad Processes In & Out of the QA Department:**  QA Processes are not well defined or are lack luster in some avenues, same goes for outside QA processes, e.g development or business processes which impact on QA.  To overcome this problem you should figure out which processes are A) Missing and begin researching how they can be implemented and B) Alert your line manager who can then bring your thoughts to perhaps the management meeting which could result in the processes being implemented and tweaked/fixed to improve effeciency.

**Lack of Resourcing:**  Estimations without QA input or the company/business promising more than can be comfortably delivered, QA department is squeezed and feels undervalued.  The best way to improve this problem is to parttake in estimations and make your concerns known to management so they can (with your help) begin correcting them.  

**Lack of or ambiguous Requirements:** The customer provide little to no help or unclear requirements, in order to overcome this problem you should try to push forward more story telling sessions and communicate with the customer making them aware that it is in both parties interests to develop clear concise criteria here, define solid entry criteria around this.

**What are the roles of QA?**


