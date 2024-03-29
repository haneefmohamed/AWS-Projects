# How to host Static Website on Amazon S3
Amazon Simple Storage Service (Amazon S3) can be used to host static Websites without a need for a Web server (at an extremely low cost). S3 buckets can be used to host the HTML, CSS and JavaScript files for entire static websites.

Introduction
A website is static when the system services used to render web pages and scripts are all client rather than server-based. On the other hand, a dynamic website relies on server-side processing, including server-side scripts such as PHP, JSP, or ASP.NET

Most websites are becoming static websites which means they run zero server side code and consist of only HTML, CSS and JavaScript. With no server side code to run, there is no reason to host them on a traditional server.

You can start by creating an Amazon S3 bucket, enabling the Amazon S3 Website hosting feature, and configuring access permissions for the bucket. After you have uploaded files and setup Website, Amazon S3 takes care of serving your content to your visitors.

Amazon Route 53: You can also use Amazon Route 53 (a managed Domain Name System (DNS) service) to point your domain to your Amazon S3 bucket.

Amazon CloudFront: You can also use Amazon CloudFront to enable your website to load quickly. Amazon CloudFront will create a content delivery network (CDN) that hosts your website content in close proximity to your users.

# Advantages of Hosting Website on S3
Here are some of the advantages of hosting site on S3

Performance: The website will be highly performant and scalable at a fraction of the cost of a traditional Web server.

Scalability: Amazon S3 is inherently scalable. For popular websites, the Amazon S3 architecture will scale seamlessly to serve thousands of HTTP requests per second without any changes to the architecture.

Availability: In addition, by hosting with Amazon S3, the website is inherently highly available.


# Set-Up Instructions
Below are the steps to deploy static Website on Amazon S3. You can follow these instructions to deploy your own static Website.

Open AWS Management console. Select S3 under Storage.

Step 1 - Create an S3 Bucket
When you first create an S3 bucket, you select the AWS Region in which the files will be geographically stored.

Click on "Create Bucket" button.

Provide a globally unique name for bucket and select Region.

Leave blank this field "Copy Settings from an existing bucket".

Create Bucket

![Screenshot 2024-02-12 170140](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/24c37d75-4851-41bb-91e0-0dcdd9bd4d59)

Step 2 - Upload Content of your Website
Upload the website contents to your S3 bucket including sub-folders.

For Example: You can use sample Website "Website" folder contents (provided in this repository).

index.html
error.html
css
images

Upload Contents

![Screenshot 2024-02-12 170208](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/f9e71ef5-f60f-4d01-95b4-2aec24e866a5)

Step 3 - Add a Bucket Policy to allow Public Read Access
Go to Permissions Tab and update Public Access Setting:

Uncheck Manage public bucket policies:

Uncheck - Block new public bucket policies (Recommended)

Uncheck - Block public and cross-account access if bucket has public policies (Recommended)

![Screenshot 2024-02-12 170252](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/9e298206-a9b9-4f27-b6ec-0b36778f5f0a)

![Screenshot 2024-02-12 170341](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/3b2c3582-b933-4823-9de6-f86062aced80)


Step 4 - Enable Website Hosting
In order to serve assets via url, you need to enable Website Hosting

Go to Properties and enable "Static Website Hosting" option

Note the endpoint. http://{bucket-name}.s3-website-{AWS-Region}.amazonaws.com

Step 5 - Access Your Website (Testing/Validation)
Access the site in browser: http://{bucket-name}.s3-website-{AWS-Region}.amazonaws.com

For Example: http://pwdgen.s3-website-us-east-1.amazonaws.com/


![Screenshot 2024-02-12 170404](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/5d4c44ef-4c50-428d-9818-9e3dc57b6f66)
