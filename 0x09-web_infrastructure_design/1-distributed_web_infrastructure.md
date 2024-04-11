Description

### Infrastructure Components:

1. **2 Servers**: These servers will be configured for different roles. One will serve as a web server running Nginx, and the other as an application server where your code base runs. This separation allows for more specialized optimization and security settings tailored to each server's specific role.

2. **1 Load Balancer (HAproxy)**: The load balancer sits in front of your servers and distributes incoming traffic between them. This helps to ensure that no single server becomes overwhelmed with requests, which can improve the performance and reliability of your website.

3. **1 Set of Application Files**: Your codebase will be replicated across the application servers to ensure that any server can handle requests for your website.

4. **1 Database (MySQL)**: The database stores the data needed by your website. It can be accessed by the application server to retrieve or store data as needed by your application.

### Explanation of Additional Elements:

- **Load Balancer**: Adding a load balancer like HAproxy is crucial for distributing incoming traffic evenly across your servers, preventing any single server from becoming a bottleneck. This improves your website's scalability and availability.

- **Distribution Algorithm**: The load balancer can be configured with various algorithms; a common choice is the round-robin algorithm. This method distributes incoming connections sequentially to the list of servers. It works simply by passing a new connection request to the next server in line, then starting over at the beginning of the list once it reaches the end. Other algorithms include least connections (directing traffic to the server with the fewest active connections) or IP hash (selecting a server based on the hash of the client’s IP address).

- **Active-Active vs. Active-Passive Setup**: 
  - In an **Active-Active** setup, all servers are handling traffic simultaneously, maximizing resource utilization and providing redundancy in case one server fails. 
  - In an **Active-Passive** setup, one server is in standby mode while the other handles all the traffic. The standby server only becomes active if the primary server fails. This setup is simpler but doesn't utilize resources as efficiently as the Active-Active setup.
  - Given the structure, using HAproxy for distributing traffic implies an Active-Active setup for the web and application servers, maximizing the efficiency and reliability of the infrastructure.

- **Database Replication (Master-Slave Cluster)**: This setup involves a primary (master) database that handles all write operations, while one or more replica (slave) databases synchronize with the master to mirror its data. The replicas handle read queries, thus distributing the database query load. This improves performance and provides data redundancy.

- **Primary Node vs. Replica Node**: In the context of the application, the primary node (master) processes all write operations (INSERT, UPDATE, DELETE) to ensure data integrity and consistency. The replica nodes (slaves), meanwhile, handle read-only operations (SELECT queries). This separation helps in scaling the database by distributing the read load.

### Infrastructure Issues - Single Points of Failure (SPOF):

- **Database**: If using a single master database without a failover replica, the database becomes a SPOF. If the master database goes down, the entire application cannot perform write operations, severely impacting the website's functionality.

- **Load Balancer**: While adding a load balancer improves traffic distribution and fault tolerance among web and application servers, the load balancer itself can become a SPOF. If it fails, the entire website could become inaccessible. To mitigate this, a secondary load balancer can be set up in an Active-Passive or even Active-Active configuration, depending on the infrastructure's complexity and needs.

