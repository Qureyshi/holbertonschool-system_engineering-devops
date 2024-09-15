Web Infrastructure Design for www.foobar.com
Infrastructure Diagram
Here's a textual description of the three-server web infrastructure with security and monitoring features:

![1_MhxvI1JIsOaWkLKkQN-QqA](https://github.com/user-attachments/assets/d6314872-1fef-4051-b82b-5ff8d68bc963)

Components and Their Purpose
Load Balancer (with SSL Termination)

Purpose: Distributes incoming traffic across multiple web servers to balance load and ensure high availability.
SSL Termination: Manages and terminates SSL connections, decrypting incoming HTTPS traffic so that web servers handle only HTTP traffic. This simplifies SSL management and improves performance on web servers.
Web Servers (3 Instances)

Purpose: Serve the website content and handle HTTP requests. Multiple instances ensure redundancy and scalability.
MySQL Database

Purpose: Stores website data. In this design, it is configured as a single write master with potential for replication to read replicas (not shown).
Firewalls (3 Instances)

Purpose: Protect different network layers. Each firewall monitors and filters traffic:
Before Load Balancer: Protects the perimeter and ensures only valid traffic reaches the load balancer.
Between Load Balancer and Web Servers: Ensures secure communication and prevents direct access to web servers.
Database Firewall: Protects the database from unauthorized access and attacks.
SSL Certificate

Purpose: Encrypts traffic between the user's browser and the load balancer, ensuring that data transmitted is secure and private.
Monitoring Clients (3 Instances)

Purpose: Collects and sends data to monitoring services (e.g., Sumologic). Helps track the health and performance of web servers and the load balancer.
Data Collection: Monitors metrics such as traffic, errors, system health, and performance, providing insights and alerts for proactive management.
Explanation of Elements
Why Add Firewalls?

Firewalls are crucial for security. They block unauthorized access and potential attacks at different network layers.
Why Serve Traffic Over HTTPS?

HTTPS encrypts data between the user and the server, protecting sensitive information from eavesdropping and tampering.
Purpose of Monitoring:

Monitoring tools track performance, uptime, and errors. They help detect issues early, allowing for quick resolution and ensuring the infrastructure runs smoothly.
How Monitoring Tools Collect Data:

Monitoring tools use agents or data collectors installed on servers to gather logs, metrics, and performance data. This data is sent to a central monitoring service for analysis and visualization.
Monitoring Web Server QPS (Queries Per Second):

To monitor QPS, configure the monitoring tool to track and report the number of queries handled by the web server over time. This involves setting up specific metrics and alerts for high query volumes.
Issues with This Infrastructure
SSL Termination at Load Balancer:

Issue: SSL termination at the load balancer means that internal traffic between the load balancer and web servers is not encrypted. This could be a security risk if internal traffic is intercepted or compromised.
Single Write Master MySQL Server:

Issue: Having a single MySQL server for write operations can create a bottleneck and a single point of failure. If this server goes down, write operations are halted, impacting data availability and performance.
Servers with Same Components:

Issue: Having web servers with identical components (web server, application server, database) can lead to resource contention and inefficiencies. For example, a high load on the database could affect the web server's performance. Ideally, web servers should handle web/application logic, while dedicated database servers manage data.
By addressing these issues and carefully designing the infrastructure, you can build a robust, secure, and scalable web application environment.

GitHub Repository Information
Repository: holbertonschool-system_engineering-devops
Directory: web_infrastructure_design
File: 2-secured_and_monitored_web_infrastructure

Feel free to explore this repository for more information on designing secure and monitored web infrastructures!
