# Serverless-Deployment

## 📖 Overview
This project demonstrates a **fully serverless** web application hosted on **AWS**. It includes:
- **Amazon S3** for static file hosting (`index.html` & JavaScript)
- **Amazon CloudFront** for fast content delivery
- **AWS Lambda** (with API Gateway) to handle GET/POST requests
- **Amazon DynamoDB** for data storage

🎯 Architecture Diagram

![diagram-export-3-1-2025-5_45_55-AM](https://github.com/user-attachments/assets/97490916-640a-4ffb-ac8a-686be3ef8040)

## 🛠 Setup Guide

### 1️⃣ **Create an S3 Bucket for Static Files
1. Go AWS console
2. Go to S3 service
3. Click **Create Bucket**
    - Name: `your-bucket-name`
    - **check** "Block all public access"
    - 
![Screenshot (746)](https://github.com/user-attachments/assets/3519aa51-4825-48e5-955c-a1abaa7021eb)

4.Upload:
   - `index.html`
   - `app.js`

![Screenshot (747)](https://github.com/user-attachments/assets/f34d7516-89f2-4d2f-86d0-8c8ee0119e44)


![Screenshot (748)](https://github.com/user-attachments/assets/e9eb0f57-2fd6-4019-8c29-45e972047184)

5. 4. **Make Bucket Public:**
   - Go to **Permissions** → **Bucket Policy**
   - Add the policy:
   ```json
   {
     "Version": "2012-10-17",
     "Statement": [
       {
         "Effect": "Allow",
         "Principal": "*",
         "Action": "s3:GetObject",
         "Resource": "arn:aws:s3:::your-bucket-name/*"
       }
     ]
   }
![Screenshot (754)](https://github.com/user-attachments/assets/08beab58-b213-468c-a5e8-738304bedcd6)

6. Note your S3 Bucket URL.

2️⃣ Set Up CloudFront (CDN)
1. Go to AWS CloudFront
   
2. Click Create Distribution

3. Origin Settings:

4. Origin Domain: Select your S3 bucket

5. Viewer Protocol Policy: Redirect HTTP to HTTPS

6. Default Cache Behavior:

7. Allowed HTTP Methods: GET, HEAD

8. Caching Policy: Use AWS Managed-CachingOptimized

9. Create Distribution (Wait for deployment)

10. Note your CloudFront URL.

    
![Screenshot (753)](https://github.com/user-attachments/assets/698004d4-155a-4939-a274-3349cd5a0197)

3️⃣ Create a Lambda Function
1. Go to AWS Lambda
   
2. Click Create Function → Choose Author from scratch

 ![Screenshot (738)](https://github.com/user-attachments/assets/ea8b1aa0-feb0-4beb-939f-7d49b851a7a3)

3.   
![Screenshot (739)](https://github.com/user-attachments/assets/36dae4d7-0e93-42cd-ba02-987be29f134b)

4.
![Screenshot (740)](https://github.com/user-attachments/assets/da5ff6c4-a71e-4dd1-a0eb-07259b4c7291)

4️⃣ Set Up API Gateway
1. Go to API Gateway

2. Click Create API → New APi
   
![Screenshot (741)](https://github.com/user-attachments/assets/c59772f4-9be8-4b52-b91f-7bfc9562708c)

3. Give Api name

4. Create GET and POST method for the lambda function
   
![Screenshot (743)](https://github.com/user-attachments/assets/6c33ec95-58b8-4e5d-b7cd-e322fd6a882f)


![Screenshot (744)](https://github.com/user-attachments/assets/c23c9cb2-ac3e-430c-b48e-410ba923f956)

5. Enable CORS for resource sharing
   
![Screenshot (745)](https://github.com/user-attachments/assets/a6bb2a99-d1ed-4905-b728-fefbb2035d9d)

5️⃣ Create a DynamoDB Table
1. Go to AWS DynamoDB

2. Click Create Table

3. Table Name: YourDynamoDBTable

4. Primary Key: id (String)

5. Click Create Table

![Screenshot (736)](https://github.com/user-attachments/assets/ae7e5683-2753-411d-9cbc-02280ca10a53)


##Attach IAM permissions to Lambda:

1. Go to IAM

2. Attach AmazonDynamoDBFullAccess to Lambda's IAM role

![Screenshot (737)](https://github.com/user-attachments/assets/568104ea-0951-4205-8977-a21d1f8b6ec3)

🌍 Final Deployment

🎯 Your static site will load from S3 which is unsecure.

![Screenshot (752)](https://github.com/user-attachments/assets/4638bdeb-e410-4570-afe6-c9bd2869fbd7)

🎯 So visit CloudFront URL to access your web app more securely.

![Screenshot (755)](https://github.com/user-attachments/assets/12169c5d-286b-40b0-97d7-1d3cb5c7d56a)



