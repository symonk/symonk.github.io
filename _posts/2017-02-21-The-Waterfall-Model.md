---
layout: post
title: 'The Waterfall Model'
bigimg: /img/path.jpg
published: false
---

In this article we will be discussing both the agile and waterfall software development life cycles (SDLC's).  We will begin with discussing the waterfall model.  Not as prevalent today as it once was.  It was one of the first development life cycles to really come into the market at a mass scale.  The Waterfall SDLC has a number of different stages, these are outlined below with a brief description
of what occurs at each stage (NB - Some diagrams/articles may reference the stages with slightly different names).  Every stage in the waterfall model requires input from the stage before it.


![Waterfall Model](/img/waterfall.png)

- Requirements - Typically at the initial stage of the process, teams would gather all possible requirements for the software to be developed.  These should be well documented and the team should have a good understanding of exactly what the customer wants and any potential problems they may face.  Outcome is typically a Requirement specification.

- Design - At this stage we use the requirements previously discussed to really drill deep into how the system is going to operate.  We would focus on hardware, software, networking & databases at this stage.  Our aim is to create a blueprint which covers all the requirements we recently outlined in stage 1.  The team will discuss how the interface / UI will look as well as designing the physical database(s), schema etc.  During this phase we would make a Design Specification Document (DSD).  This will set the guidelines for what we are about to make.  The DSD document will include information such as the project scope, designs, process & data design, user interface information and many others.

- Implementation - At this stage the team will use the Design Specificiation Document is used to create smaller parts of the system, referred to as "units".  Each unit is individually developed and tested for its functionality, this is also known as "unit testing".  In the next stage these units are brought together and this is typically known as integration testing.

- Integration & Testing - Previously developed units start coming together at this stage to shape the finished software.  Here we will focus on how the units interact with each other specifically and observe any weird behaviours (even if they are not linked to each other heavily).  After the Integration the entire system is tested for any faults or failures.

- Deployment - Once all functional and or non functional testing has been done, the product is deployed into the customers environment or released into the market.  There can also be some UAT (User Acceptance Testing) going on at this stage.

- Maintenance - Ongoing maintenance of the system, any issues which come up in the client environment.  To fix these generally a patch is released.  The team may also want to upgrade the version to make tweaks and or improvements, maintenance is done to deliver these changes to the customer(s) environment(s).
