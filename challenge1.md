# Challenge number 1 - BUCKETS OF FUN

## Challenge Statement
The challenge statement that you are working on this lab focused on analyzing an IAM policy, understanding its permissions, and using the AWS CLI to find and retrieve a flag stored in an S3 bucket.

## IAM Policy
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::thebigiamchallenge-storage-9979f4b/*"
        },
        {
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:ListBucket",
            "Resource": "arn:aws:s3:::thebigiamchallenge-storage-9979f4b",
            "Condition": {
                "StringLike": {
                    "s3:prefix": "files/*"
                }
            }
        }
    ]
}
```
### write a short analysis about the IAM policy here
```
* What do I have access to?
- Get and list the objects from s3 bucket

* What don't I have access to?
- Other locations apart from the bucket

* What do I find interesting?
- The entire challenge was intresting to me because the concept of s3 buckets is something new to me which I always wanted to know about but never had a chance until now.
```

## Solution
1. Analyzing the IAM Policy
   - The policy had two `Action` keys: `s3:GetObject` and `s3:ListBucket`. These actions allow listing and retrieving files in the S3 bucket.  

2. Using AWS CLI to Interact with the Bucket
   - Following the AWS CLI guide, I listed the objects in the bucket using the below command which showed two files: `flag1.txt` and `logo.png`.
     ```
     aws s3 ls s3://thebigiamchallenge-storage-9979f4b/files/

   - I retrieved the flag file with:
     ```
     aws s3 cp s3://thebigiamchallenge-storage-9979f4b/files/flag1.txt -

3. Checking the Flag 
   - I pasted my flag in the `Insert flag` text box, completing the challenge.


## Reflection
* What was your approach?
  ```
  - Analyse Research Analyse Repeat
* What was the biggest challenge?
  ```
  - Finding the flag, I was thought the policy would give everything I wanted, I recognized a pattern in the policy but failed to get the flag.
* How did you overcome the challenges?
  ```
  - I referred AWS cli guide provide to accquire the flag.
* What led to the break through?
```- Reading the Lab question for the final time.```

* On the blue side, how can the learning be used to properly defend the important assets?
  ```
  - Always pay extra attention while configuring access to users.
