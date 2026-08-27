# ecommerce-traditional-vs-serverless
Comparing traditional server-based and serverless AWS architectures for a scalable e-commerce application.


## Project Overview
The purpose of this project was to design and compare two different architectures for an e-commerce application: a traditional server-based architecture and a serverless architecture using AWS services.

The aim was to understand the trade-offs between the two approaches, including differences in cost, scaling, fault detection, maintenance and management. I also explored how each architecture responds when errors or failures occur, what parts of the application could be affected, and how each design would handle changes in traffic and demand.

By comparing both approaches, I was able to understand why the choice of architecture depends on the requirements of the application rather than one approach simply being better than the other.

## Traditional Architecture

![Traditional Architecture](diagrams/week%203%20traditional%20architecture%20e-commerce%20project.png)
The traditional architecture uses multiple server-based components to handle traffic and run the e-commerce application.

A user first accesses the application through Amazon Route 53, which provides DNS routing and directs the request towards the application. Amazon CloudFront is then used as a content delivery network (CDN), caching content closer to users so that frequently requested content can be delivered with lower latency.

Incoming traffic is distributed across the web servers using an Application Load Balancer. This prevents a single web server from receiving all of the traffic and helps the application remain available as demand increases.

The web tier then communicates with the application tier through an internal load balancer, which distributes requests across the application servers. These servers handle the backend processing required by the e-commerce application.

The application servers communicate with the database to store and retrieve application data. A cache is also used for frequently accessed data, reducing the need to repeatedly retrieve the same information directly from the database. Amazon S3 provides object storage for content such as product images, documents and other files.

To handle changes in demand, the web servers and application servers are placed within Auto Scaling Groups. Amazon CloudWatch monitors metrics and can trigger scaling policies when defined thresholds are reached. The Auto Scaling Groups can then add or remove EC2 instances depending on the amount of capacity required.

This architecture provides greater control over the underlying servers and infrastructure, but it also requires more infrastructure to be managed and monitored compared with the serverless design.


