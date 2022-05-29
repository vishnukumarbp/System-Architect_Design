# Software Architecture, System Design and Big data processing ([COURSE LINK](https://nagarro.udemy.com/course/software-architecture-design-of-modern-large-scale-systems/))
## System Architecture

#### Definition:
A high level description about the _system structure_, _its components_ and _how those components interact with each other_ to meet the system _requirements_ and _constrainst_

##### _system structure:_
High level structure of the end production with its components. No detail about technologies and programming languages

##### _requirements:_
How the components together comes to do what system described to do

##### _constraints:_
How well the structure/architecture is designed to not do the constraints

#### Level of Abastractions:
In System architecuture, there are different level of abstractions
1. Classes/Structs
2. Modules/packages/libraries
3. Services (processes/group of processes)


#### Software Development cycle
Design phase is where the system is architected. Architectue is the Output of the Design Phase, and input to the implementation phase.
<img width="1142" alt="image" src="https://user-images.githubusercontent.com/10495294/170851914-4458b237-3f58-43ab-b690-d136a06492c0.png">

### Requirements:
- Requirement **Gathering**
- Requirement **Classification**

##### **_Gathering:_**
Typical world, Requirements are format document describing the end goal of the product we need to build.
Large scale system requiremnet is different from the abstracted requirement we get.

SO First ask as much as questions around the requirement before start architecture. 
For eg: 

**Requirement:**
_Build ride sharing feature/app_

**Question to ask:**
_Is it going to be a mobile app?_
_Are we going to implement payment gateway?_
_Live tracting of the status?_
_pre book feature?_

##### **_Classification:_**
Classify the requirement beased on three different categories, also refered as Architectural Drivers
1. Functional Requirement: Features of the System
2. Non Functional Requirement: Quality Attirbutes of the System
3. Limitation and boundaries: System contraints

##### **1. Functional Requirement:**
Features of the system. these doesnt dictate the System architecture. These fuctions/features takes input or action and output result

##### **2. Non Functional Requirement:**
Quality Attirbutes of the System, and this dictates the architecture of the system. few to name,
Scalability, Availability, Reliability, Performance, Security...

##### **3. System contraints:**
Limitation and boundaries to consider while design the architecture
Time limit constraints, staffing constraints, budget constraints etc.,


### Feature Requirement: Step by Step Process

#### Gathering Requiremnet:
Asking all the questions for the large scale product is not the right approach. There are different methods to gather requiremnets.

More powerful methods of the requirement gatherings are,
- Use Cases : Scenario / Situation our system is used
- User flows : A Step by Step / graphical representation of use cases.


##### Requirement gathering steps:
- Identify all the actors/users in the system
- Capture and describe the all the possible use cases
- User Flow: expand each use cases through flow of events and events contains (ACTION & DATA)

These steps are represented using UML or Sequence diagram. Sequance diagration is a visual documentation of interaction between actor and the different component of the system. 
These diagram helps to design the API interaction required from the the actors. 

