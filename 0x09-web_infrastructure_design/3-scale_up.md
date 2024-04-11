 Updated Infrastructure Components:

1. **1 Server (Application Server)**: This new server is dedicated solely to running the backend application logic. It interacts with the database and executes the application code, processing business logic, making CRUD operations (Create, Read, Update, Delete) to the database, and returning the data back to the web server.

2. **1 Load Balancer (HAproxy)**: An additional HAproxy load balancer is configured in a cluster with the existing one to ensure high availability and reliability. This setup ensures that if one load balancer fails, the other can take over, preventing a single point of failure.

3. **Split Components**:
   - **Web Server**: Its own server is tasked with handling HTTP requests from clients, delivering static content, and acting as the intermediary between the user and the application server. It can also perform tasks like SSL termination to offload these operations from the application server.
   - **Application Server**: Separated onto its own server, it focuses on executing application logic, interacting with the database, and processing dynamic content. This separation allows for more efficient resource utilization and easier scaling of the application layer independent of the web serving layer.
   - **Database**: Hosted on its own server, the database management system (DBMS) stores and retrieves all the data needed by the application. Isolating the database onto its own server maximizes performance and security, allowing for dedicated resources and more stringent security measures.

 Additional Elements and Their Purposes:

- **Dedicated Application Server**: Adding a dedicated server for the application logic allows for more efficient processing and the ability to scale the application independently from the web server. This is particularly useful for complex applications that require significant resources for data processing and execution of business logic.

