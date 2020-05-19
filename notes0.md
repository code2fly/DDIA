# Reliable , Scalable and Maintainable Applications

Main characterstics of good apps - 
![alt](/resources/images/basic_rsma.PNG)


### Introduction - 
---------------

- Today applications are data intensive as opposed to compute intensive.
- Problems with apps today are ***amount of data***, ***complexity of data***, ***speed at which it is changing***.
- we will see what data systems have in common or what distinguishes them and how they achieve those characterstics.
- there are many database systems with different characterstics as diff apps have different requirements, there are various approaches to caching(like write-through etc..) or ways of building search indexes and so on. We just need to figure out which approach is best for task in hand.
- different data systems like db,cache,queue etc though being in differnt categories have a superficial similarity i.e. they all store data for some time. But they have different access patterns, which means difference performance characterstics and diff impl.
***So why are they all together under one umbrella term Data systems???***
  - many news tools for data storage and processing do not come under single category. e.g. Data stores like Redis are also used as MQ or MQ's like kafka with db like durability.
  - apps today have wide ranging of requirements that a single tool is not able to fulfil data storage and processing needs and different tools have to be stiched together using app code.
    - for e.g. as below we have a caching layer, full text search server(elasticsearch or solr) seperate from our main db. then its our app code's responsibility to keep them in sync.
    ![alt](/resources/images/basic_samplearch.PNG)


- When designing data system or service(by combining serveral tools inorder to provide a service) the main concerns are - 
  - ***to ensure data remains correct and complete even when things go wrong internally?***
  - ***how do we handle an increase in load***
  - 3 main concerns that are important in most software systems - 
    - **Reliability** - the system should continue to work correctly even in case of h/w or s/w faults or human errors.
    - **Scalability** - as system grows(in data volume, traffic volume) there should be reasonable ways of dealing with that growth.
    - **Maintanability** - over time people should be able to work on system productively.


### 1. Reliability -
  - it roughly means continuing to work correctly, even when things go wrong(also called faults).
    - system that can cope with these faults are called fault tolerant or resilient.
    - fault is not the same as failure, fault is when one component of a system stops working as expected while failure is when the system as a whole stops providing the required service to user.
      - faults probability can never be reduced to 0, therefore design fault-tolerant mechanism that can prevent faults from causing failure.
    - These fault tolerant systems can be well tested by using ***Chaos Engineering*** (like Chaos Monkey).
    - the kinds of faults that we will be dealing with are - 
      - Hardware fault - hard disk crashing , ram faults, power issues etc..
        - this can be improved by adding redundancy
        - but since cloud systems are made to prioritize flexibility and elasticity over single machine reliability, hence ***there is a move towards systems that can tolerate entire machine failures with software fault tolerance techniques in addition to hardware redundancy***.

      - Software errors - these faults cause systemetic errors within system causing more system failures than h/w faults. 
        - a s/w bug that can cause app server to crash given a bad input.
        - a runaway process that uses up a shared resource like CPU,memory,n/w bandwidth etc..
        - a service on which system is dependent slows down or becomes unresponsive or starts returning corrupted results (e.g. query attributes :D )
        - cascading fault where a fault in one component triggers fault in another component and so on.
        - there is no quick solutions to these s/w bugs - 
          - carefully thinking about assumptions and interactions in system.
          - thorough testing, process isolation, allowing process to crash and restart.

      - Human errors - making software reliable with unreliable humans.
        - design in a way to minimize error opportunities - use well design abstractions, API and admin interfaces.
        - test thoroughly
        - allow quick and easy recovery from human errors to minimize impact in case of failure - making it fast to rollback config changes , rollout new features gradually to a subset of users.
        - setup detailed clear monitoring , such as performance metrics and error rates (telemetry).  

### 2. Scalability -
  - one common reason for software degradation is increased load (perhaps more concurrent users ).
  - scalability is described as a systems ability to cope up with increased load.
  - load can be described in terms of ***load parameters*** 
    - choice of these parameters depends on architecture of system
      - can be requests/second to a web server
      - ratio of reads to writes in a database
      - number of simultaneous users in a chat room.
      - hit rate on cache or something else...

  - **twitter example describing load parameters and how scalability was attained with increased load** -   
  
### 3. Maintanability - 
