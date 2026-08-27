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

## Serverless Architecture

![Serverless Architecture](diagrams/week%203%20serverless%20architecture%20e-commerce%20-%20diagram.png)
The serverless architecture replaces the traditional web and application server tiers with managed AWS services that can respond to requests and events without requiring the same level of server management.

A user first accesses the application through Amazon Route 53, which provides DNS routing. The request then reaches Amazon CloudFront, which acts as a content delivery network (CDN) and can cache content closer to users to reduce latency.

Amazon S3 is used to store static content such as product images and other files, while CloudFront can cache and deliver this content efficiently to users.

Dynamic application requests are sent through Amazon API Gateway, which acts as the entry point for the backend API and routes requests to the appropriate AWS Lambda function.

The backend is divided into separate Lambda functions for searching products, adding products to a basket, and placing an order. Each function performs a specific task and runs in response to the relevant request or event.

Amazon Cognito is used for authentication and authorisation, helping to verify users before they access protected application functionality.

Amazon DynamoDB stores the main application data, including products, baskets and orders.

When an order is placed, the Place Order Lambda can generate an event that is sent to Amazon EventBridge. EventBridge then routes the event to other services. Amazon SES (Simple Email Service) can send an order confirmation email, while Amazon SQS (Simple Queue Service) can queue fulfilment work so that dispatch processes can handle orders asynchronously.

Amazon CloudWatch provides monitoring, logs and alarms for the serverless application.

This design reduces the amount of infrastructure that needs to be directly managed and allows services such as Lambda and DynamoDB to scale automatically as demand changes.




