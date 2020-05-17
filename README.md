# AWS-Cloudformation-static-website-s3-cloudfront-route53
## Goal
A cloud formation template that creates a static website that uses a custom domain to server traffic through a cloud front distribution with website static asserts hosted in an s3 bucket.
## Periquisites 
    * [Python]
    * [AWS Command Line Interface] 
You must configure the default credential for use with [AWS Command Line Interface] 
```shell script
$ aws configure
```
## Usage 
```shell script
aws cloudformation create-stack --stack-name myteststack --template-body file:///home/testuser/mytemplate.yaml --parameters DomainName=Parm1,FullDomainName=test1 ParameterKey=Parm2,AcmCertificateArn=test2
{
  "StackId" : "arn:aws:cloudformation:us-west-2:123456789012:stack/myteststack/330b0120-1771-11e4-af37-50ba1b98bea6"
}
```
###### Template Properties
* DomainName - The DNS name of an existing Amazon Route 53 hosted zone e.g kellyaudu.me
* FullDomainName - The full domain name e.g www.kellyaudu.io
* AcmCertificateArn - The Amazon Resource Name (ARN) of an AWS certificate(Certificate must be created in us-east-1 region)
###### Resources to be created
* WebsiteBucket - An S3 bucket with a public read permission that stores the static assets of the website
* WebsiteBucketPolicy - Creates a bucket policy for the website bucket with a  public read permission 
* WebsiteCloudFront - Creates a CloudFront distribution with the website bucket as it's origin and serves traffic to the public via the custom domain 
* WebsiteDNSName - Adds an Alias recordset to route53 with DNS Name pointing to the domain name of the CloudFront distribution
###### Outputs from operation
* BucketName - Name of s3 bucket that stores website content
* CloudfrontEndPoint - Endpoint for CloudFront distribution
* FullDomainName - Full DomainName
## Validate template
```shell script
aws cloudformation validate-template --template-url file:///home/testuser/mytemplate.yaml 
{
    "Description": "A cloud formation template that creates a static website that uses a custom domain to server traffic through a cloud front distribution with website static asserts hosted in an s3 bucket.:",
    "Parameters": [],
    "Capabilities": []
}
```
[AWS Command Line Interface]:http://aws.amazon.com/cli/
[Python]:https://www.python.org/
