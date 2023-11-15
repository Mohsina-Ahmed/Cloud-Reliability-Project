<h1 align="center">
Reliability Project
</h1>

<p align='center'>This repo contains the files for my final project at Makers Academy as part of the Cloud/DevOps Engineering specialism track.</p>

## Project Overview

In this project, our team collaborated with an organization providing software and services to multiple veterinary hospitals. The main objective was to improve the reliability of their current application, HOSP, while preserving its core functionality. We also took on the task of introducing enhancements and integrating new features to enhance the overall user experience.

## The HOSP system (Load balancer and API documentation)

Regrettably, we lacked access to the source code due to licensing constraints. However, we did have entry to the load balancer on AWS and comprehensive API documentation</br>
![HOSP Diagram](/diagrams/HOSP-diagram.jpg)

## Approach and Investigation

Our primary concentration was on fortifying the system's reliability. In response to user-reported issues, we probed into the matter using Amazon CloudWatch to scrutinize the application logs. This exploration unveiled a notable surge in unsuccessful API requests at the server endpoints. This pivotal revelation empowered us to identify the underlying triggers of the challenges faced by users.

## Implementation of NGINX Reverse Proxy Server

In addressing the issue of unsuccessful API requests, we introduced an NGINX reverse proxy server deployed on an AWS EC2 instance. Two NGINX servers operated concurrently in this approach, strategically engineered to initiate automatic retries for failed requests (500/502). The outcome was a substantial decrease in the overall failure rate. Through the implementation of this solution, we successfully bolstered the system's resilience, leading to a more seamless user experience. We encountered a challenge when attempting to integrate SSL certificates with NGINX, as the one obtained from ACM was incompatible for use with NGINX. Consequently, we transitioned to CloudFront to address this issue.

![dashboard](/diagrams/dashboard.png)

## Implemented Improvements Tickets

With the system's reliability significantly enhanced, we shifted our focus to implementing several crucial improvements tickets:

1. **Enhanced Security with HTTPS:**
   To bolster the security of the system, our primary focus was on implementing the HTTPS protocol. This pivotal initiative entailed the deployment of an AWS CloudFront CDN to enforce encrypted communication throughout all traffic. The shift to HTTPS played a crucial role in elevating data privacy, ensuring the protection of sensitive information exchanged within the system.

   In close collaboration with corporate IT, we meticulously strategized the migration process with the aim of minimizing downtime during the transition to the new domain. Effectively directing traffic to the newly secured HTTPS-enabled domain, we ensured uninterrupted service for users, simultaneously strengthening the overall security of the system.

2. **Screening Results Integration:**
   In response to a specific request from hospital nurses, we implemented a feature that facilitated the direct saving of screening results into patient notes. Previously, these results lacked archival on the HOSP server, and our enhancement streamlined the process, contributing to a more comprehensive patient record.

   To realize this improvement, we devised an intricate solution leveraging AWS Lambda and Python. We developed a Lambda function with the capability to capture the API response from the screening server. Subsequently, the function initiated a new POST request back to the patient notes endpoint. This request was meticulously crafted, incorporating the patient ID within the header and encapsulating the X-Ray results as a structured JSON payload—all while ensuring the seamless delivery of the original request back to the user.

3. **Audit Trail Functionality:**
   To enhance system transparency and security, we introduced an audit trail feature that empowered system administrators to monitor all user activities closely. This functionality offered a comprehensive overview of user interactions, facilitating the prompt identification of potential security breaches and enabling swift corrective actions.

   The implementation of the audit trail feature involved the use of an AWS Lambda function. We created a new API route dedicated to querying AWS Athena with a specific SQL command against a CloudWatch database. The results of this query were subsequently provided as a unique URL, allowing administrators to download the audit trail as a CSV file for in-depth analysis.

![Improvements diagram](/diagrams/cloudfront-lambdas.jpg)

These enhancements collectively advanced the system's functionality, user experience, and security standards, establishing a robust and seamless operation for both hospital staff and patients. Through the utilization of serverless technology, we guaranteed the system's effortless adaptation to escalating demands, eliminating the burdens associated with traditional server maintenance. This approach not only improved scalability but also substantially decreased operational overheads. Hospital staff and patients enjoyed the benefits of a consistently reliable, high-performing system, enabling them to concentrate on their core tasks without any interruptions.

## Final System Diagram

![Final diagram](/diagrams/Final-diagram.jpg)
