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

