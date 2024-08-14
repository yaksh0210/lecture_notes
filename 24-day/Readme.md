# Notes

## Aws-Cli

<img src="./images/aws_cli.png">


### AWS CLI Access

### What is AWS CLI?

+ AWS Command Line Interface (CLI) is a unified tool to manage AWS services from the command line.

+ Installation:

+  Installable on various platforms (Windows, macOS, Linux) via package managers or downloadable installers.

```sh
sudo apt-get update
```

```sh
sudo apt-get install awscli
```

```sh
aws --version
```


### Configuration:

+ Use aws configure command to set up access keys, secret keys, region, and output format.

```sh
aws configure
```

+ configuration:

    + Access Key ID: Your AWS access key.
    + Secret Access Key: Your AWS secret access key.
    + Default region name: E.g., us-west-2.
    + Default output format: E.g., json.


### Authentication:

+ Access to AWS services is managed through IAM (Identity and Access Management) roles and policies.

### Commands:

+ Allows you to execute commands to manage AWS resources (e.g., S3, EC2, IAM) using simple syntax.

### Scripting:

+ AWS CLI commands can be integrated into scripts for automation and efficient resource management.

### Output Formats:

+ Supports JSON, text, and table formats for command outputs, allowing for easier parsing and readability.



## S3 in Aws

<img src="./images/bucket.png">

<br>

### What is Amazon S3?

+ Amazon Simple Storage Service (Amazon S3) is a scalable object storage service provided by Amazon Web Services (AWS). It allows users to store and retrieve any amount of data from anywhere on the web. S3 is designed to offer high durability, availability, and scalability.

### Key Features of Amazon S3

***Scalability:***


+ Automatic Scaling: S3 automatically scales to handle growing amounts of data. You don't need to provision or manage storage capacity.

+ High Capacity: Can store an unlimited amount of data and objects.

***Durability:***

+ High Durability: S3 is designed for 99.999999999% (11 9's) durability over a given year. Data is redundantly stored across multiple facilities.

***Availability:***

+ High Availability: S3 provides high availability with a service level agreement (SLA) of 99.9% uptime.

***Data Security:***


+ Access Control: You can set permissions and access controls at both the bucket and object levels using policies, bucket ACLs (Access Control Lists), and IAM (Identity and Access Management) roles.

+ Encryption: Supports server-side encryption (SSE) for data at rest and SSL/TLS for data in transit.

***Data Management:***


+ Lifecycle Policies: Automatically manage objects through policies that move data between different storage classes or delete it after a specified period.

+ Versioning: Keep multiple versions of an object, allowing you to recover from unintended overwrites or deletions.

***Cost Efficiency:***

+ Storage Classes: Offers different storage classes such as Standard, Intelligent-Tiering, One Zone-IA (Infrequent Access), Glacier, and Glacier Deep Archive, each with different cost structures based on access patterns and data retrieval needs.



### Common Uses of Amazon S3

**1. Backup and Restore:**

+ Use S3 for backup and archival storage solutions. It’s commonly used for storing backup data and disaster recovery plans.

**2. Data Archiving:**

+ Archive data that is infrequently accessed but needs to be preserved, such as historical data or compliance-related records.

**3. Big Data Analytics:**

+ Store large datasets for analysis using tools like Amazon Athena, Amazon Redshift Spectrum, or Hadoop.

**4. Content Distribution:**

+ Serve static web content, such as images, videos, and documents, often integrated with content delivery networks (CDNs) like Amazon CloudFront.

**5. Application Data:**

+ Store application data, logs, and files in a scalable and cost-effective way.

**6. Disaster Recovery:**

+ Implement disaster recovery strategies by storing copies of critical data in geographically dispersed S3 buckets.


<hr>

### 1. Create Bucket

**Definition:**
+ A bucket is a container for storing objects in Amazon S3.

### Steps:
+ Sign in to the AWS Management Console.
+ Go to the S3 service.
+ Click "Create bucket."
+ Enter a unique name for the bucket and select a region.
+ Configure options like versioning, logging, and tags.
+ Set permissions and choose any additional settings.
+ Click "Create bucket" to finalize.

### 2. Upload Objects

**Definition:**

+ Objects are files and their metadata stored in a bucket.

### Steps:

+ Go to the S3 service in the AWS Management Console.
+ Open the desired bucket.
+ Click "Upload."
+ Drag and drop files or use the file picker to select files.
+ Configure upload options like permissions and storage class.
+ Click "Upload" to complete the process.

### 3. Give Public Access

**Definition:** 

+ Public access allows anyone on the internet to view or download the objects in your bucket.

### Steps:

+ Go to the S3 service and open your bucket.
+ Click on "Permissions" tab.
+ Edit the "Bucket Policy" or "Access Control List (ACL)" to allow public access.
+ Example Bucket Policy for public read access:

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
```
+ Ensure the "Block public access" settings are configured correctly to allow public access.

### 4. Storage Class

**Definition:** 

+ Storage classes are different types of storage options in S3 with varying costs and retrieval times.

### Types:

+ Standard: For frequently accessed data.
+ Intelligent-Tiering: Moves data between two access tiers when access patterns change.
+ One Zone-IA: For infrequent access, but in a single availability zone.
+ Glacier: For archival storage with retrieval times in minutes to hours.
+ Glacier Deep Archive: Lowest cost for long-term archival storage.
+ Selection: Choose based on access frequency, cost considerations, and retrieval needs.

### 5. Pricing

**Definition:** 

+ Pricing is based on the amount of data stored, the number of requests, and data transfer out.

### Components:

+ Storage Costs: Charged per GB per month.
+ Requests and Data Retrieval: Charges for PUT, GET, and other operations.
+ Data Transfer: Costs for data transferred out of S3 to the internet or other AWS regions.
+ Additional Costs: For features like cross-region replication or lifecycle transitions.

### 6. Lifecycle Management

**Definition:** 

+ Automatically manages your objects to optimize costs and compliance by transitioning or expiring objects.

### Features:

+ Transition Actions: Move objects between storage classes based on age or other criteria.
+ Expiration Actions: Automatically delete objects after a certain period.

### Configuration:

+ Go to the "Management" tab of your bucket.
+ Click "Create lifecycle rule."
+ Define the scope (e.g., prefix or tag).
+ Set transition and expiration rules as needed.
+ Review and create the rule.

### 7. Host a Static Website on S3

**Definition:** 

+ Serve static web content like HTML, CSS, and JavaScript from an S3 bucket.

### Steps:

+ Create and configure a bucket to host a static website:
  
    + Go to the S3 service and open your bucket.
  
    + Go to the "Properties" tab.
  
    + Enable "Static website hosting."
  
    + Specify the index document (e.g., index.html) and optionally an error document.
  
    + Upload your static website files to the bucket.
  
    + Configure bucket permissions to allow public access to the objects.
  
    + Access your website using the S3 endpoint URL provided in the static website hosting settings.
  
     
