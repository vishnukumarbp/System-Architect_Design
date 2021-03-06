# Software Architecture, System Design and Big data processing ([COURSE LINK](https://nagarro.udemy.com/course/software-architecture-design-of-modern-large-scale-systems/))
## System Architecture

#### Definition:
A high level description about the _system structure_, _its components_ and _how those components interact with each other_ to meet the system _requirements_ and _constrainst_

##### _system structure:_
High level structure of the end product with its components. No detail about technologies and programming languages

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
Scalability, Availability, Reliability, Performance, Security... [More details](https://github.com/vishnukumarbp/System-Architect_Design/blob/main/README.md#non-functional-requirement-quality-attributes) 

##### **3. System contraints:**
Limitation and boundaries to consider while design the architecture
Time limit constraints, staffing constraints, budget constraints etc., [More details](https://github.com/vishnukumarbp/System-Architect_Design/blob/main/README.md#system-constraints) 


### Functional Requirement: Step by Step Process

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
Provides the quality measures on how well our system perform on a particular dimension. Architecture of the system is designed/redesigned mainly because of the non functional requirements (quality attributes of the system). 
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
    - Regulatory constraints are hard to skip, but with right justification we can extend the deadline or budget. 
    - Once we accept the constraint, it is very hard to skip them once we have build the system
    - so spend enough time to decide on the constraints before starting
* Use loosely coupled architecture
    - Rather creating tightly coupled architecture between our application and third party apis, creating a loosely coupled archecture, so that we can change if required in the later run.


## Quality Attributes in Details
Quality Attributes is huge. We will be focusing on those important attributes in details used in large scale architecture.
1. Performance
2. Scalability
3. Availability

others are, Maintainability, Deployability, Usabiliy, Testability, Reliability, Portability, Security etc.,

### Performance:
This is measured by Response time and throughput, 

##### Response Time (End to End Latency): 
ie, time taken between a client sending a request and receiving the response.

`Response Time = Processing Time + Waiting Time (latency)` 

_Processing Time -> Amount of time spend on our system to process, query, build response_
_Waiting Time (sometime referred as latency) -> Duration of the time request/response spends **inactively** on our system, i.e, network latency, gateways, and queues_


##### Throughput:
- Amount of work/task performed by the system at a time
   * measured by task per second
- or Amount of data processed by the system per unit of time
   * measured by bits/sec, bytes/sec, mbytes/sec, gb/sec
    

#### Considerations:
1. Measure the response time correctly.
2. Response time distribution
3. Performance Degradation

##### **1. Measure the response time correctly:**
Calculate both processing and waiting time to derive response time/avg response time

##### **2. Response time distribution:**
To measure the response time and derive the performance, we can use Response time distribution. 
Recommended to use Histogram to derive the percentile distribution chart.
Percentile distributions is `the xth percentile is the value below which x% of the value can be found`

<img width="1084" alt="image" src="https://user-images.githubusercontent.com/10495294/170855912-31c5b64e-b605-4b7f-990d-dec1ff7d5d3c.png">

**Tail Latency**
<img width="1084" alt="image" src="https://user-images.githubusercontent.com/10495294/170855927-1657d237-e83c-4905-ba90-d3daeae7df43.png">
Shorter the tail latency better the response time (performance)

--- Considerations
Define the response time goal using percentiles, for eg: 30ms at 95th percentiles of the response time

Measure and compare the goal using percentailes distributions

##### **3. Performance Degradation:**
Degradation point from where the performance starting degrade significantly as the load increases (Refer below graph)

<img width="1084" alt="image" src="https://user-images.githubusercontent.com/10495294/170856218-efd2756f-2693-4096-9304-fcb72c5b3305.png">

There could two way it degrades, drastically, or gradually.
Drastically means, High utilizations of resources. for eg:
* High CPU utilization
* High Memory utilization
* Message queues at capacity
* Maximum number of IO connections
* ...


### Scalability:

The measure of a system ability to the growing amount of work, in an easy and cost effective ways by adding more resources to the system.

When we plot amount of work vs resources, we have to get linear Scalability (not 100%)

There are three orthogonal types of scalability:
1. Vertical (Scale Up)
2. Horizontal (Scale Out)
3. Team/Organization


#### 1. Vertical Scalability
Adding or upgrading resources on a single computer, to allow our system to handle higher traffic or load

For eg: Increasing the database's CPU or memory or network card for higher bandwidth

**Pro:**
* Any application can benefit from this
* No code changes required
* Migrations is very easy as it is in the same computer

**Cons:**
* Scope is limited
* Centralized system (single point of failure), so cannot provide High Availability, and Fault Tolerance

#### 2. Horizontal Scalability
Adding more computer (machine) with required resources to handle in a distributed way

**Pros:**
* No limit on scalability
* It is easy to add/remove machines
* If designed correctly, we can get High Availability, and Fault Tolerance

**Cons:**
* Initial code changes to support distributed system
* Increase complexity and coordination overhead

#### 3. Team/Organizational Scalability
The measure of a system ability to the growing amount of work **(features, testing, bug fixes, releases)**, in an easy and cost effective ways by adding more resources **(Engineers)** to the system.

So increasing engineers working on a system will help to scale the system faster. but adding more and more engineers will eventually degrade the performance.
or break code base into monolithic into multiple services.


### Availablity:
Most important attribute while designing a system. A fraction of time/probability that our service is operationally functional and accessible to the end user.

`Availability (%) = uptime / (uptime + downtime)`

MTBF => Mean Time Between Failure (Uptime)
- Represent the avg operation time
- Useful, when dealing with multiple hardward and its shelf life
- not calculated when dealin with cloud or thrid part api

MTTR => Mean Time To Recover
- Time average takes us to detect and recover from a failure
- Average downtime

`Availability (%) = MTBF / (MTBF + MTTR)`

It has impact on both Users and Business.

If user faces issues while accessing our system or while making payment, we lose customers. it has more impact when the system is health or aircraft releated, we put users life in danger.

Similarly, if the business provides services to other business and provide low available product, they lose businesses. it will have impact on overall business.

90% is a high number, but in reality, 2h 24m and 36 days in a year is not acceptable.
99.9 is referred as 3 "nines"
99.99 is referred as 4 "nines"
<img width="1084" alt="image" src="https://user-images.githubusercontent.com/10495294/170861938-3c96150a-98e9-42e8-939b-57492f09be5d.png">


### Fault Tolerance and High Availabilty
#### What Prevent us from Achieving HA - Source of Failure
1. Humar Error
    * Pushing wrong config, running wrong cmd, untested code
2. Software Error
    * Long garbage collection, out of memory error, null pointer exception, segmentation faults
3. Hardware failures
    * Due shelf life, hardware (servers, routers, storage) breaking down, power outages, network failures because of - infra issues and general congestions 

#### How to achieve Hight Availabilty?
Failures will happen despite adding process around Human errors. 
Fault Tolerance is the way to get High Availability.

#### Fault Tolerance:
Fault Tolerance enables our system to remain operational and available to users despite failures within one ore multiple components.

It revolves around 3 tactics:
1. Failure Prevention
2. Failure detection and isolation
3. Recovery

##### 1. Failure Prevention:
- Eliminate Single point of failure through Replications (store multiple replica in multiple db) and Redundancy (running multiple instance of service)
    * Spatial Redundancy -> Replicas of our application in multiple instances
    * Time Redundancy -> Retry the request multiple time until it succeed or give up
    * Two stragies used widely in the industry are
        - Active - Active architecture (multiple replica to store)
        - Active - Passive Architecture (primary and secondary)

##### 2. Failure detection and isolation:
If any one of our system failed for any reaosn, it should be detect and isolated so that no further request is passed to it.
to detect, we will have monitoring system, which will be keeping tract of each servers in the network for your system availabilty through heart beat or health checks. It can sometime isolate an healthy system just because of network or any communication issues. Those are called **False-Positive**. But is fine until it does reverse when system is failed, but not detected.

##### 3. Recovery:
Actions after detecting faulty instance/server:
    - Stop sending more workload
    - Restart the server
    - Rollback - rolling back to the stable version

## SLA, SLO, SLI

### SLA:
**Service Level Agreement** between service provider and Client/User (it is an legal agreement)

Promise made to our Users interms of our quality service we provide
- Avaialbilty
- Performance
- Data durability
- Time to response to system failures

It also states, the pernalities and financial consequences if we fail to meet.

### SLO:
**Service Level Objectives:** Individual Goal set for our system. Each SLO represent a target value/range we need to meet. 

For eg:
- Availability of 3 nines,
- Average response time SLO to be less than 100ms at the 90th percentiles
- Issue resolutions time between 24 and 48 hours


### SLI:
**Service Level Indicators:** Quantitative measures of our compliances with SLO's
It is the actutal numbers measured from monitoring systems or logs


## API (Application Programming Interface):
When designing our application, we will have a black box which contains two parts, 
- Behaviour
- Interface

Behaviour is well defined. and interfaces through which external application or client application can communicate with the service.

there are three categories of API's
1. Public APIs (open APIs which can be accessed by anyone, but suggsted to have users registered to have control over)
2. Private/Internal APIs (exposed to only selected services or interal services of the organization)
3. Partner APIs (Exposed to only subscribed users/company)

### RPC
### REST (https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm)



## LOAD BALANCER:

This is an widely used component of system design almost 100% of the high volumn system. 
Load balancer, as its name suggested, it is used to balanace the load (distribute) across multiple instances of the application. 

### Quality Attributes
Load balancer act as an abstract server which provides,
- Scalability - Scaling features (auto scaling)
- Performance - Mayb Add a little latency, but it is acceptable cost
- High Availability - We can have monitoring features to detect and resolve unavailable instances
- Maintainability - Since we can add and remove instances, new release can be rolled out easily one by one, called Rolling Release



### Types of Load Balancer
1. DNS (Domain Name System) Load Balancing
2. Hardware Load Balancing
3. Software Load Balancing
4. Global Server Load Balancing


#### DNS Load Balancing:
DNS is part of Network Infrastructure. Used to resolve domain name to IP Addresses. One domain name can have mapping to multiple ip addresses. Phone book of the Internet.
Comes as part of domain name, for free. but has few drawbacks. 
- It doesnt monitor the health of our servers
- Uses simple round robin strategy as balancing stragies, which doesnt help if one of our server is high performant or overloaded
- Less secures, as it exposes the ip address to client application


#### Hardware and Software Load Balancing
Both are similar in their nature, and only difference is that we will have dedicated device designed and optimized to do only load balancing in hardware load balancing, while software load balancing is just a program designed to do load balancing which can run on any general purpose computer.

Only the IP address of the load balancer is exposed to client application and load balancer will redirect the request to one or multiple services intelligently based on their
- Health
- Current load on the server
- Number of open connections
- its processing power

One more important feature is that, 
It can be used for internal communications incase of microservice architecture. where each service will act as an abastraction to multiple instance of particular service, and they can communicate with each other using the load balancer.

Load balancer and servers are co-located. else we will be adding extra latency to the request and response.
But in case of multiple data centers, we have to accept this latency as we will have the load balancer co-located to only one data center.

This type of load balancer still need DNS to resolve to ip address. to overcome this issue, we have one more load balancer which is an hybrid between these two.

#### Global Server Load Balancing:

It is an hybrid between:
DNS and Hardware/software load balancing.

GSLB is an smart DNS service running between client applications and load balancers. Each request will go through GSLB which resolves the domain name to ip addresses.
Most GSLB can be configured to route the traffic based on varity of strategies not just by physical locations.
Since, GSLB is in constant communication with data centers, it can route the traffic based on,
- nearby data center
- Best-estimated response time
- CPU load in each data center
- Bandwidth between user and the data center


#### [Load balancing Solutions](https://nagarro.udemy.com/course/software-architecture-design-of-modern-large-scale-systems/learn/lecture/29603416#overview)


## MESSAGE BROKERS:
Most fundamental building blocks for any Asynchronous Software Architecture.

opposite of Synchronous communication where both sender and receiver should be in sync constantly to complete a request, it will get worse if the processing time is considerably longer.

Message Broker: A software architectural building block which uses queued data structure to store messages between senders and receivers.

It provides, 
- Asynchronous Architecture
- Buffering

Generally Message broker follows Pub/Sub Pattern to store and stream messages. Multiple services can subscribe to single topic/message and perform asynchronous task. 

In terms of Fault Tolarence, Message Broker provides High Availability by superior fault tolarence by storing messages in queue and stream when services are back online and prevents messages being lost.

It add a little performance latency, as it adds significant indirection to two services

#### [Solutions Available](https://nagarro.udemy.com/course/software-architecture-design-of-modern-large-scale-systems/learn/lecture/29617964#overview)

## API Gateway:
API gateway is an service setup between client and server to redirect request based on the resource. This is used mainly when we have multiple services (micro services) handling tasks independently, client application has to call each services separately and should be aware of all the available services and its uri. By using API gateway, client can directly connect to API Gateway and request the resource. API Gateway will be aware of the available services, it will make call to each services and collect the response and responde it to the client.


API Gateway follows API composition pattern to compose single api from collection of multiple api's from services.


API Gateway works on Layer 7, i.e API Gateway will have the data and request uri, so it can directly work with the request uri and its data. on the other hand load balancer works are network layer (where it can read the data or uri)

### Benifits:
1. seamless integration/modification of internal service, For eg. if we want to support mobile devices, we can create service mobile apps, and redirect from api gateway, this way our web isnt affected
2. Consolidating all the security, authentication and authorization in a single place
3. Depending on the users permission, we can allow or redirect request to authorized services
4. Rate limiting to avoid DoS
5. Request Routing -> Single call to api gateway, and gateway will collect response from multiple services
6. Caching
7. Monitering and alerting
8. Protocol Translation -> Client to API Gateway might use REST JSON, but API Gateway to service can be gRPC or SOAP

### Anti Pattern
- Never make api gatewat smart by adding business logic into it
- API Gateway will become single point of failure, to avoid, deploy multiple instances of api gateway and place them behind the load balancer
- By adding API Gateway we may add a small latency to the request, this might tempt sometime to bypass the api gateway, which is considered as anti pattern

#### [Solutions Availables](https://nagarro.udemy.com/course/software-architecture-design-of-modern-large-scale-systems/learn/lecture/29629912#overview)


## CDN (Content Delivery Network):

CDN is a globally distributed network of servers which are strategically placed in various locations and speed up the delivery of the static content to the end users. CDN uses caching technique to cache the static content in multiple locations (which are called Edge). Based on the Users of the application, we can configure the Edge locations where the contents can be cached to reduce the latency between each request and allow the content to be loaded fast. 

By using CDN, we can achieve, 
- Performance - Faster page loads
- High Availability - issues/slowness are less noticible, and cached content can still be serverd when the system is down
- Security - Protection against Distributed Denial of Service attact (DDoS) as the attach is blocked at CDN level

Static contents are, Images, Videos, HTML, CSS files and JavaScript

### Content Publishing Strategies:
1. Pull Strategy
   - We need to tell CDN how offen the content need to be refreshed (cached) by setting TTL on each content
   - Advantages: Lower maintenance, as we have to just set TTL, everything else is taken care of by CDN
   - Disadvantages: When the content isnt cached, the first request by the user will take longer time to be served as CDN will load content from the server
   - When the content is changed frequently, pull strategy is better
2. Push Strategy
   - It is our/server responsibility to push the content to CDN if the content need to be cached, and purge the cache if the content is changed
   - Advantages: High Availability, Avoid the spike on the request as the server is responsible for updating the cache content
   - Disadvantages: If any content is changing frequently, server has to publish new content to CDN more frequently

#### [Solutions Availables](https://nagarro.udemy.com/course/software-architecture-design-of-modern-large-scale-systems/learn/lecture/29629954#overview)

