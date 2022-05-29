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
Features of the system. these doesnt dictate the System architecture. These fuctions/features takes input or action and output result [More details](https://github.com/vishnukumarbp/System-Architect_Design/blob/main/README.md#feature-requirement-step-by-step-process)

##### **2. Non Functional Requirement:**
Quality Attirbutes of the System, and this dictates the architecture of the system. few to name,
Scalability, Availability, Reliability, Performance, Security... [More details](https://github.com/vishnukumarbp/System-Architect_Design/blob/main/README.md#quality-attributes) 

##### **3. System contraints:**
Limitation and boundaries to consider while design the architecture
Time limit constraints, staffing constraints, budget constraints etc., [More details](https://github.com/vishnukumarbp/System-Architect_Design/blob/main/README.md#system-constraints) 


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


### Non Functional Requirement (Quality Attributes):
Provides the quality measures on how well our system perform on a particular dimension
Architecture of the system is designed/redesigned mainly because of the non functional requirements (quality attributes of the system). 
For eg: system is redesigned when
it is not fast enough
not secure
hart to maintain
not scalable
slow to develop

Examples:
Availability Quality attribute
Online store must be **available** for user to request for atleast **99.9% of the time**

Deployability quality attribute
Development team can **deploy new version** of the product atleast **twice a week**

#### Considerations:
- Quality attributes need to be **MEASURABLE** **TESTABLE** (for eg: api response in <1 sec)
- Tradeoffs
    * there isnt a single architecture which satisfies all the requirements
    * certain attributes contradict with one another
    * Some combination is very hard to achieve or impossible
    * As an architect we have to make RIGHT TRADEOFF based on the priority and importance to achieve the highest chance for success
- Feasibility - Feasibility of the requirement, either technically impossible or prohibitively expensive to implement. for eg: expecting 100% availability, and high quality streaming on low bandwidth area


### System Constraints:
A System constraints is essentially a decision that was already either fully or partially made for us, restricting our degrees of freedom.

Three type of constraints:
1. Technical Constraints (Particular programming language, infra license, limited resources) - In many cases they do affect the decision we make for our architecture. For eg, for security reason, having on premises infra, makes cloud architecuturea / paradigm and solutions unavailable for us. 
2. Business Constraints (Limited budget and deadline, first to market)
3. Regulatory/Legal Constraints (in US HIPAA, in Europe GDPR)

#### Considerations:
* We shouldnt take any constraints lightly
    - Regulatory constraints are hard to skip, but with right justification we have extend the deadline or budget. 
    - Once we accept the constraint, it is very hard to skip them once we have build the system
    - so spend enough time to decide on the constraints before starting
* Use loosely coupled architecture
    - Rather creating tightly coupled architecture between our application and third party apis, creating a loosely coupled archecture, so that we can change if required i the later run.




