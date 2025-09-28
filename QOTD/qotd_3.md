Question: What is Infrastructure as Code (IaC) and why is it important in DevOps?

Answer: Infrastructure as Code (IaC) is a practice in DevOps that involves managing, and provisioning IT infrastructure through machine-readable definition files rather than physical hardware configuration or traditional interactive configuration tools. It represents the IT infrastructure and configuration in code form. 

IaC is crucial because, firstly, it enables version control for infrastructure, which allows you to keep track of changes, understand what has been modified, and even revert changes if necessary. Secondly, it supports consistency in environments, eliminating the discrepancies between development, testing, and production environments. Thirdly, IaC enables automation, reducing the need for manual configuration and reducing the likelihood of errors and inconsistencies. Lastly, it boosts productivity, as the DevOps teams can quickly set up and replicate infrastructure at scale.

Diagram/Example: A simple example of an IaC script using AWS CloudFormation:

```yaml
Resources:
  MyBucket:
    Type: 'AWS::S3::Bucket'
    Properties:
      BucketName: 'my-example-bucket'
      AccessControl: 'PublicRead'
``` 

This IaC script example will provision an S3 Bucket on AWS, set its name as 'my-example-bucket', and make it publicly readable. The benefit here is that this script can be reused to create an identical S3 bucket with the same properties, ensuring consistency and saving time compared to manual setup.

