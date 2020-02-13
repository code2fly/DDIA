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
    - **Maintanabilty** - over time people should be able to work on system productively.