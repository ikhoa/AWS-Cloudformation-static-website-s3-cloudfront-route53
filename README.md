# AWS-Cloudformation-static-website-s3-cloudfront-route53
A cloud formation template that creates a static website that uses a custom domain to server traffic through a cloud front distribution with website static asserts hosted in an s3 bucket.
######Properties
* DomainName - The DNS name of an existing Amazon Route 53 hosted zone e.g kellyaudu.me
* FullDomainName - The full domain name e.g www.kellyaudu.io
* AcmCertificateArn - The Amazon Resource Name (ARN) of an AWS certificate(Certificate must be created in us-east-1 region)
###### Resources
* WebsiteBucket - An S3 bucket with a public read permission that stores the static asserts of the website
* WebsiteBucketPolicy - Creates a bucket policy for the website bucket with a  public read permission 
* WebsiteCloudFront - Creates a cloudfront distribution with the website bucket as it's origin and serves traffic to the public via the custom domain 
* WebsiteDNSName - Adds an Alias record set to route53 with DNS Name pointing to the domain name of the cloudfront distribution
###### Outputs
* BucketName - Name of s3 bucket that stores website content
* CloudfrontEndPoint - Endpoint for cloudfront distribution
* FullDomainName - Full DomainName
