Difficulty: Moderate
Tech Stack: AWS, Terraform
Question: Your company uses AWS for its infrastructure and Terraform for infrastructure orchestration. One day, you notice that Terraform is frequently timing out when attempting to create an AWS RDS instance, and it's impacting the deployment process. What steps would you take to diagnose and address this issue?
Hint: Consider how you can adjust Terraform timeouts and look at options to debug logs. Investigate the performance of AWS services as well.
Answer: I would approach the problem in several steps.

1. Enable verbose logging in Terraform: By setting `TF_LOG` environment variable to `DEBUG` or `TRACE`, we enable detailed logging in Terraform. This can reveal additional details about the cause of the timeout error. 

```bash
export TF_LOG=DEBUG
terraform apply
```

2. Check the AWS status page: It's valuable to verify if there are any ongoing issues with AWS services, specifically RDS, in the relevant region. AWS status page provides this information.

3. Adjust the Terraform timeouts: Terraform supports customization of specific timeouts for resources. In the case of `aws_db_instance`, we can increase `create` timeout as such:

```hcl
resource "aws_db_instance" "default" {
  ...
  timeouts {
    create = "60m"
    delete = "2h"
  }
}
```
This code snippet tells Terraform to wait 60 minutes for the RDS instance creation before timing out.

4. Check the AWS account limits: If the AWS account has hit its limit on the number of RDS instances, creation of new instances will fail. AWS Management Console can be used to verify this.

5. Network issues: It’s important to investigate if any network issues between the Terraform host and AWS are causing the timeouts. Tools like `traceroute`, `ping`, or `mtr` can be utilised for this.

6. Validate IAM permissions: Make sure the IAM role used by Terraform has the necessary permissions to create an RDS instance.

If all these steps don't help to resolve the issue, it would be a good idea to raise a support ticket with AWS including as many details possible from the investigation. 

Diagram/Example: Not applicable