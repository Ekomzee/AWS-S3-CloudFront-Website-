# AWS-S3-CloudFront-Website-Deployment

This project demonstrates how to deploy a static website on AWS using S3 for hosting and CloudFront as a CDN.

## Prerequisites
- An AWS account with permissions for S3 and CloudFront.

## Setup Steps

1. **Create an S3 Bucket**
   - Create a uniquely named bucket.
   - Disable "Block all public access."
   - Enable Static Website Hosting and set `index.html` as the index document.

2. **Upload Website Files**
   - Upload your `index.html` and any other required files (CSS, JS, images) to the S3 bucket.

3. **Set Bucket Policy**
   - Add a bucket policy to allow public read access:
     ```json
     {
         "Version": "2012-10-17",
         "Statement": [
             {
                 "Sid": "PublicReadGetObject",
                 "Effect": "Allow",
                 "Principal": "*",
                 "Action": "s3:GetObject",
                 "Resource": "arn:aws:s3:::your-bucket-name/*"
             }
         ]
     }
     ```
   - Replace `your-bucket-name` with your actual bucket name.

4. **Create a CloudFront Distribution**
   - In the CloudFront console, create a new distribution.
   - Set the Origin Domain Name to your S3 Website Endpoint.
   - Configure caching and viewer protocol settings as needed.
   - Wait for the distribution to deploy (this may take ~15 minutes).

5. **Test Your Website**
   - Copy the CloudFront Distribution Domain Name and paste it into your browser to see your live website.

## Cleanup
- To remove all resources, delete the CloudFront distribution and then empty and delete the S3 bucket.
