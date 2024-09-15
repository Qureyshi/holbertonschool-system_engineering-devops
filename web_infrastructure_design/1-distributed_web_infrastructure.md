Distributed Web Infrastructure Design
Diagram
Here’s a textual representation of a three-server web infrastructure setup for www.foobar.com:

![t2](https://github.com/user-attachments/assets/9fc1ad07-06ac-49ce-a6b5-49f41561fe64)

Explanation of Components
User's Browser:

The user initiates an HTTP request to www.foobar.com.
Load Balancer (HAProxy):

Role: Distributes incoming requests across multiple web servers to balance the load.
Distribution Algorithm: Common algorithms include Round-Robin (which distributes requests sequentially) or Least Connections (which sends requests to the server with the fewest active connections).
Active-Active vs. Active-Passive:
Active-Active: All servers handle requests simultaneously. This improves load distribution and fault tolerance.
Active-Passive: Only one server handles requests while others are on standby. This setup is less complex but doesn’t distribute load evenly.
Configuration: Typically, HAProxy can be configured for an Active-Active setup where all web servers handle traffic.
Web Servers (Nginx):

Role: Handle HTTP requests and serve static content. They also interface with the application server to process dynamic requests.
Application Files: Contain HTML, CSS, JavaScript, and PHP scripts needed to generate web pages.
Application Server:

Role: Executes application code, processes requests, and interacts with the database.
Configuration: This can be on the same server as Nginx or a separate server, depending on how resources are allocated.
Database (MySQL):

Primary-Replica Cluster:
Primary Node: Handles all write operations and updates. It is the main source of truth for the database.
Replica Node: Handles read operations and can be used for backup. Replicas are updated with changes from the Primary Node, providing read scalability and redundancy.
Replication: The Primary Node sends changes to the Replica Nodes to keep them in sync.
Issues with This Infrastructure
Single Points of Failure (SPOF):

Load Balancer: If the load balancer fails, the entire system becomes unavailable unless a failover solution is implemented.
Primary Database Node: If the Primary Node fails, write operations cannot be performed.
Security Issues:

No Firewall: Without a firewall, the servers are exposed to potential security threats from the internet.
No HTTPS: Data transferred between the user's browser and the web server is not encrypted, making it vulnerable to interception.
No Monitoring:

Lack of Monitoring: Without monitoring tools, it’s difficult to track server performance, detect issues, or get alerted about potential problems.
Summary
This distributed infrastructure design aims to balance the load between multiple web servers, ensuring improved performance and redundancy. However, it introduces new complexities, such as potential SPOFs and security vulnerabilities, which need to be addressed to create a robust and secure web environment.
