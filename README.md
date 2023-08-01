## Automated Deployment of AWS Resources for Medicaid forms data extraction and visualization solution Using AWS CloudFormation

This repository contains the sample CloudFormation template for the AWS  blog post - Medicaid forms data extraction and visualization solution. The template provisions required AWS Services ( Lambda functions, AWS Glue Tables,Amazon Athena queries, SNS Topics, S3 buckets) for the solution. 

## Solution Architecture

![Overall Architecture Diagram](./docs/arch-overview.PNG "Overall Architecture Diagram")

The following section describes the architecture components in the above architecture and how each service functions within the solution. 

1.	Scanned image of the paper based claim is uploaded to Amazon S3 bucket. This triggers a Amazon Simple Notification Service (Amazon SNS) message and invokes the AWS    Lambda Function.
2.	The AWS Lambda function’s call to Amazon Textract is made asynchronously. This is especially useful for processing multi-page documents, which may take time, thereby    avoiding issues related timeouts. The response to the Asynchronous operation is a job identifier (JobId). The Amazon Textract asynchronous API is configured to send    a notification to Amazon SNS when the processing of documents is completed.
3.	The notification to Amazon SNS triggers an AWS Lambda function that uses the JobId to retrieve processed content from Amazon Textract and save the results to another    bucket in Amazon S3.
4.	AWS Glue is used to catalog the data and Amazon Athena is used to query the extracted data.
5.	Amazon Quicksight is used to display the dashboard that displays the visuals/insights derived from the extracted data in near real time. 

## Security

See [CONTRIBUTING](CONTRIBUTING.md#security-issue-notifications) for more information.

## License

This library is licensed under the MIT-0 License. See the LICENSE file.

