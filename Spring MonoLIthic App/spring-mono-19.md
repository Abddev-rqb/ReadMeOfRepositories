# Spring Boot Monolithic Deployment on AWS

## Table of Contents
- [Overview of AWS and Setting up AWS Account](#overview-of-aws-and-setting-up-aws-account)
- [Setting up RDS in AWS Console](#setting-up-rds-in-aws-console)
- [Preparing Our Spring Boot Application for Deployment](#preparing-our-spring-boot-application-for-deployment)
- [Point Your Application to Amazon RDS](#point-your-application-to-amazon-rds)
- [Creating JAR File for Our Application](#creating-jar-file-for-our-application)
- [Deploying APIs on Elastic Beanstalk](#deploying-apis-on-elastic-beanstalk)
- [Conclusion](#conclusion)

---

## Overview of AWS and Setting up AWS Account
Amazon Web Services (AWS) is a cloud computing platform that offers various services for deploying, managing, and scaling applications. AWS provides a pay-as-you-go pricing model and supports multiple architectures, including monolithic and microservices-based applications.

### Steps to Set Up an AWS Account:
1. Visit [AWS Sign Up](https://aws.amazon.com/)
2. Click on "Create an AWS Account."
3. Enter your email, password, and account details.
4. Provide billing information and verify your identity.
5. Select a support plan (free tier is available).
6. Log in to the AWS Management Console.

---

## Setting up RDS in AWS Console
Amazon RDS (Relational Database Service) provides managed database instances. We will configure an RDS instance for our Spring Boot application.

### Steps:
1. Navigate to **AWS Console > RDS**
2. Click **Create Database**
3. Choose **Standard Create** and select **MySQL/PostgreSQL**
4. Set **DB Instance Identifier**, **Master Username**, and **Password**
5. Choose instance type (free-tier eligible: `db.t2.micro`)
6. Set storage size (recommended: 20GB)
7. Configure **VPC security group** to allow inbound traffic on port **3306** (MySQL) or **5432** (PostgreSQL)
8. Click **Create Database**
9. Once created, copy the **endpoint URL** for database connection

---

## Preparing Our Spring Boot Application for Deployment
Spring Boot provides flexibility for deploying monolithic applications. We need to configure the application before deploying it to AWS.

### Steps:
1. Ensure you have `spring-boot-starter-web` and `spring-boot-starter-data-jpa` dependencies in `pom.xml`
2. Modify `application.properties` or `application.yml` to use Amazon RDS
3. Ensure your application uses **environment variables** to handle sensitive database credentials

---

## Point Your Application to Amazon RDS
Edit `application.properties` file:
```properties
spring.datasource.url=jdbc:mysql://your-rds-endpoint:3306/yourdbname
spring.datasource.username=yourusername
spring.datasource.password=yourpassword
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.jpa.hibernate.ddl-auto=update
```

For PostgreSQL:
```properties
spring.datasource.url=jdbc:postgresql://your-rds-endpoint:5432/yourdbname
spring.datasource.username=yourusername
spring.datasource.password=yourpassword
spring.datasource.driver-class-name=org.postgresql.Driver
spring.jpa.hibernate.ddl-auto=update
```

---

## Creating JAR File for Our Application
1. Open a terminal and navigate to the project root directory
2. Run the following command to create an executable JAR file:
   ```sh
   mvn clean package
   ```
3. The JAR file will be located in `target/` directory (e.g., `target/app.jar`)

---

## Deploying APIs on Elastic Beanstalk
AWS Elastic Beanstalk simplifies the deployment of applications by managing infrastructure automatically.

### Steps:
1. Install AWS Elastic Beanstalk CLI:
   ```sh
   pip install awsebcli --upgrade --user
   ```
2. Initialize Elastic Beanstalk project:
   ```sh
   eb init
   ```
   - Select AWS region
   - Choose **Java** as the platform
   - Configure SSH key (optional)
3. Create an environment and deploy:
   ```sh
   eb create springboot-env
   ```
   ```sh
   eb deploy
   ```
4. Once deployed, obtain the URL from AWS Elastic Beanstalk console and test your API:
   ```sh
   curl http://your-app-url/api/endpoint
   ```

---

## Conclusion
This guide covered the step-by-step process of deploying a Spring Boot monolithic application on AWS using RDS for database management and Elastic Beanstalk for application hosting. With this setup, you can scale your monolithic application efficiently while leveraging AWS's robust infrastructure.

For further improvements:
- Implement **CI/CD pipelines** using AWS CodePipeline
- Use **CloudWatch** for logging and monitoring
- Enable **Auto Scaling** for better performance and cost-efficiency

---

📍 **Author**: Abdul Raqeeb  
📧 **Contact**: abduloy25@gmail.com 
🔗 **GitHub**: [GITHUB_link](https://github.com/Abddev-rqb)