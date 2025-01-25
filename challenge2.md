# Challenge number #2 - Analytics  

## Challenge Statement
The challenge required analyzing an IAM policy, identifying permissions, and retrieving the flag from an SQS queue using the AWS CLI.

## IAM Policy
```json
{
    	"Version": "2012-1e-17",
	"Statement" : [
		{
			"Effect": "Allow",
			"Principal": "*"
			"Action": [
				"sqs : Sendt4essage" ,
				" sqs : Receivemessage"
			],

			"Resource": "arn:aws:sqs:us-east-1:092297851374:wiz-tbic-analytics-sqs-queue-ca7a1b2" 
		}
	]
}
```
### write a short analysis about the IAM policy here
```
Access Granted: Sending (sqs:SendMessage) and receiving messages (sqs:ReceiveMessage) from the queue.
Access Denied: Queue deletion, creation, or permission changes.
Observation: The wildcard ("*" for Principal) exposes the queue to anyone.
```

## Solution

1. List Queues
Used the AWS CLI to identify the target queue:
aws sqs list-queues

Resulted in:
https://sqs.us-east-1.amazonaws.com/123456789012/bigiamchallenge-queue


2. Receive Messages
Retrieved the flag from the queue:
aws sqs receive-message --queue-url https://sqs.us-east-1.amazonaws.com/123456789012/bigiamchallenge-queue

Resulted in:
Webpage link where the flag is retrived.

## Reflection

Analyzed the policy, identified SQS permissions, and retrieved the flag using sqs:ReceiveMessage. Initially unclear on how to use the AWS CLI for SQS; solved by reading the documentation. Realized the flag would be stored in the queue messages. Use specific principals, apply least privilege, and audit IAM policies regularly.
