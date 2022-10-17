# UPSTAC-SOLUTION

Task-1: Create an IAM role, a security group and launch an EC2 instance.

Create a EC2 Instance in default VPC and Attach the IAM role with ‘AmazonEC2ContainerRegistryFullAccess’.
Create a Security Group for UPSTAC application services.

Task-2: Install Maven and Docker-Engine on the EC2 instance and create Docker images for the UPSTAC application microservices.

Launch the EC2 instance on local terminal with SSH keypair and Install Docker-Engine.
Clone the UPSTAC application code from the GitHub repository
Create jar files for the UPSTAC application microservices using Maven.
Write a Dockerfile for all the microservices (front-end + back-end) of the UPSTAC application.
Use the Docker command to create Docker images for all the microservices of the UPSTAC application.

Task-3: Create ECR repositories and push the Docker images to ECR

Install the AWS CLI on the EC2 Instance.
Use the AWS CLI to create ECR repositories for the UPSTAC microservices.
Tag the UPSTAC application Docker images using the corresponding repository Uris noted from the output of step (2).
Push the Docker images of the microservices to the respective ECR repositories.

Task-4: Create the application load balancer and define the forwarding rules for the front-end microservices of the UPSTAC application by defining the target group.
            

Create a security group by the name ‘upstacsg’, which will allow traffic towards all the UPSTAC services:
Front-end service port:3000
Document service port:8082
Master service port:8080
Registration service port:8090
MySQL service port:3306
Application load balancer listener port:8080
Create the application load balancer by the name ‘UPSTAC_ALB’ specifying ‘upstacsg’ as the security group.
Create a target group, which represents the front-end service towards which traffic will be directed by the load balancer.

Task-5: Create an ECS service for each service of the UPSTAC application, including the MySQL database, with the AWS Fargate launch type.
Create an ECS cluster by the name ‘UPSTAC_Cluster’ using the Fargate launch type.
Create the task definition for all the services of the UPSTAC application by referencing the corresponding ECR repository and provide appropriate environment variables as input 
Create an ECS service for each microservice of the UPSTAC application by specifying ‘upstacsg’ as a security group
Enable service discovery for all the ECS services and define ‘upgrad.com’ as namespace.
Configure autoscaling for the registration microservice with minimum task as 1 and maximum task as 2 and the ECS service metrics ‘CPUUtilization’ with a target value of 5%. (Note: The ideal threshold for CPU Utilization alarms is around 70%–80%. For this assignment, its value has been kept low for facilitating the next task)
Use the ‘dig’ command to verify that the registration microservice is accessible from the Ubuntu EC2 instance with the service name <registrationservicename>.<namespace>.


Task-6: Trigger email notification for CPU Utilization > 5 % alarm and initiate autoscaling for the registration microservice of the UPSTAC application.

Create an alarm ‘upstac_regsvc_cpu_utilization_above_5percentage’ using the ECS CPU Utilization metrics for the registration service in the Fargate mode ECS cluster Define CPU Utilization greater than 5% as the alarm condition and specify the email address to receive the notification through AWS SNS as soon as the alarm condition is reached. Create a new SNS topic while defining the alarm by the name ‘UPSTAC_CloudWatch_Alarms_Topic’ .
Install Apache Benchmark on the Ubuntu EC2 compute instance.
Pump traffic (HTTP POST) towards the registration service so as to reach the alarm condition for autoscaling as well as email notification, i.e., ‘CPUUtilized’ > 5%.
Verify that email notification is received at the configured email address and the number of tasks for the registration service scales up to 2.

