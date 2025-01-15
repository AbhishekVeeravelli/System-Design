# System Design

What is System Design?

- System Design is basically the process of designing a system as well as there interaction and relationships, in order to satisfy specified requirements
- Below given headings and techniques are helpful in designing reliable distributed systems  and they are the key concepts of System Design
- The key characteristics of distributed systems include Scalability, Reliability, Availability, Efficiency and Manageability.

## **1. Scalability:**

Scalability ****is basically handling the growing amount of load by adding the resources to the system, which is managing the increasing demand

1. The system that can evolve by growing amount of data 
2. A system can grow in many different dimensions 

       Eg: 1. Growth in UserBase 

         2.  Growth in number of features of the system

         3.  Growth in volume of the data

         4. Growth in Complexity(Like a system started as simple application is grown into different smaller applications)

         5.  Growth in Geographic Reach etc.

### **Scaling a System**

- Scaling a system is basically upgrading the system. There are different ways to scale a system
1. **Vertical Scaling(Scale Up)**
- This means adding more power to the system in all possible ways. In terms of RAM, CPU Power,Storage etc. This approach will be useful for simple architecture but still have limitations on how far we can go
1. **Horizontal Scaling(Scale Out):**
- This means adding more machines to the system to spread the workload across multiple systems and considered as most effective way to scale large systems
- Eg: Netflix uses horizontal scaling for its streaming services by adding more no.of clusters to handle growing number of users and data traffic
1. **Load Balancing**
- Load balancing is process of distributing the traffic to the different servers to make sure that no single server becomes overwhelmed
- Eg: Google uses load balancing extensively across its global infrastructure to distribute search queries and traffic across its massive server farms
1. **Caching**
- Caching is a technique to store frequently accessed data in-memory(RAM) to reduce the load on the server/database and Implementing caching drastically improves response time.
- Eg: Reddit uses caching concept to store frequently accessed content hot posts and comments which can be served quickly without querying db every time.
1. **Content Delivery Network(CDN)**
- CDN distributes static assets(images,videos) closer to the users this is helpful in reducing the latency and result in faster load times
- Eg: Cloud fare provides CDN services speeding up website access for user worldwide by caching the content in servers located close to users
1. **Partitioning**
- Partitioning is basically splitting the data/functionality across multiple nodes/servers to distribute work load in order to avoid bottle necks
- Eg: Amazon DynamoDB uses partitioning to distribute the data and traffic for its NoSQL database across many servers ensuring fast performance and scalability
1. **Asynchronous Communication**
- Asynchronous communication means postponing/delaying the noncritical/long running tasks to background queues or message brokers
- Eg: Slack uses Asynchronous Communication because when a message is sent the senders interface don’t freeze it stays responsive while the message is being delivered in the background
1. **MicroService Architecture**
- Micro-service architecture breakdowns the application into smaller independent services that can be scaled independently. This also improves resilience and helps teams work on specific components in parallel
- Eg: Uber uses micro-service architecture it handles independent functions like billing, notifications, ride matching etc. which helps in efficient scaling and rapid growth
1. **Auto Scaling**
- Auto Scaling means automatically adjust the number of active servers based on the current load. This helps in handling the spikes in traffic without manual intervention
- Eg: AWS auto scaling monitors the applications and automatically adjusts the capacity to maintain steady predictable performance at lowest cost possible
1. **Multi region Deployment**
- Deploying the application in multiple data centers /cloud regions to reduce latency and improve redundancy
- Eg: Spotify uses multi region deployment to ensure music streaming service highly available and responsive to users anywhere in world

## 2. Availability

1. Availability is defined as the amount of time the system is operational and accessible when required
2. It is usually expressed as percentage, indicating the systems up time over a specific period
    
                
    
            **$Availability = Uptime / (Uptime+Downtime)$**
    

### Strategies of Improving Availability

1. **Redundancy:**
- Redundancy involves having backup component that can take over when primary component fails
- There are 3 types of Redundancies

       1. Server Redundancy: Deploying the multiple servers to handle the requests, ensuring that if one server fails the other can continue to provide the service

  2. Database Redundancy: Creating the replica of the database if the primary db fails

   3. Geographic Redundancy:  Distributing resources across multiple geographic locations to mitigate the impact of regional failure

1. **Load Balancing:**
- Load Balancing is one of the mechanism which distributes the traffic across a cluster of servers to improve the responsiveness and availability of applications/websites/DB’s etc.
- LB also tracks the status of each resources along with distributing requests
- If server is not available to take a new request or not responding or has the elevated error rate the LB will not send the traffic to such server
- LB always bound to do two tasks one is it balances the applications traffic by distributing across multiple servers and prevents application server from becoming a single point of failure by reducing server load
- To utilise the full scalability and redundancy, we can try to balance the load at each layer of the system. We can add LB’s at three places

          1. Between Client and web server

    2. Between web server and internal platform layer like application server/cache servers

    3. Between internal platform layer and DB

- There are two types of LB’s
    
       1. Hardware Load Balancers : These are the physical devices to distribute the traffic based on pre configured rules
    
        2. Software Load Balancers: These are the software solutions that manage traffic distribution, such as cloud based solutions like AWS load balancer
    

**Advantages of LB**

- Faster User Experience, Uninterrupted service
- Service providers experience less downtime and higher throughput
- Helps in handling the incoming requests while decreasing the wait time for users
- Smart LB’s gives the actionable insights to the organisations by predicting the traffic bottle necks before they happen
1. **FailOver Mechanism**
- Failover mechanism automatically switches to a redundant system when failure is detected

        1. Active passive failover: When a active server fails the passive server which is on standby takes over upon failure

    2. Active-Active failover: All components are active and share the load if one fails the remaining component continue to handle the load seamlessly

1. **Data Replication:**  This involves copying data from one location to another to ensure the data is available even if anyone fails

        Synchronous Replication: Data is replicated in real time to ensure consistency across locations

   Asynchronous Replication: Data is replicated with a delay, which may be efficient but can have slight data inconsistency

1. **Monitoring and Alerts**
- Continuous health monitoring requires checking the status of the system components to detect the failure early and trigger the alerts for immediate actions
- There are different techniques like Heartbeat Signals,Health checks and Alerting systems

### **Best Practices for High Availability**

1. Design for failure: Always assume any component can fail at anytime design the system accordingly
2. Implement health checks: Do regular health checks and respond to issue before becoming critical
3. Use Multiple Availability zone
4. Practice Chaos Engineering: Intentionally send failures to test
5. Implement circuit breakers: Prevent cascading failures by cutting off problematic service  
6. Caching wisely: Caching can improve the availability by reducing load on backend systems
7. Plan for Capacity: Ensure system can handle expected and unexpected load increases
8. By implementing strategies like redundancy, load balancing, failover mechanism and data replication helps in high availability of systems

## CAP Theorem

- CAP Stands for Consistency, Availability and Partitioning Tolerance
- This theorem states that it is impossible for a distributed data store to simultaneously provide all three guarantees.

       1. Consistency(C): Every read receives the most recent write or an error.

 2. Availability(A): Every request receives a  non-error response without guarantee that it contains most recent write.

 3. Partition Tolerance(P) : The system continues to operate despite an arbitrary number of messages  being dropped(or delayed) by the network between the nodes.