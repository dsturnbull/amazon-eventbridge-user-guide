# AWS Events<a name="aws-events"></a>

The following is an example event in Amazon EventBridge\.

```
{
  "version": "0",
  "id": "6a7e8feb-b491-4cf7-a9f1-bf3703467718",
  "detail-type": "EC2 Instance State-change Notification",
  "source": "aws.ec2",
  "account": "111122223333",
  "time": "2017-12-22T18:43:48Z",
  "region": "us-west-1",
  "resources": [
    "arn:aws:ec2:us-west-1:123456789012:instance/ i-1234567890abcdef0"
  ],
  "detail": {
    "instance-id": " i-1234567890abcdef0",
    "state": "terminated"
  }
}
```

It is important to remember the following details about an event:
+ They all have the same top\-level fields – the ones appearing in the example above – which are never absent\.
+ The contents of the **detail** top\-level field are different depending on which service generated the event and what the event is\. The combination of the **source** and **detail\-type** fields serves to identify the fields and values found in the **detail** field\. For examples of events generated by AWS services, see [EventBridge Event Examples from Supported AWS Services](event-types.md)\. 

Each event field is described below\.

**version**  
By default, this is set to 0 \(zero\) in all events\.

**id**  
A unique value is generated for every event\. This can be helpful in tracing events as they move through rules to targets, and are processed\.

**detail\-type**  
Identifies, in combination with the **source** field, the fields and values that appear in the **detail** field\.  
All events that are delivered via CloudTrail have `AWS API Call via CloudTrail` as the value for `detail-type`\. For more information, see [Events Delivered Via CloudTrail](event-types.md#events-for-services-not-listed)\.

**source**  
Identifies the service that sourced the event\. All events sourced from within AWS begin with "aws\." Customer\-generated events can have any value here, as long as it doesn't begin with "aws\." We recommend the use of Java package\-name style reverse domain\-name strings\.  
To find the correct value for `source` for an AWS service, see the table in [AWS Service Namespaces](https://docs.aws.amazon.com/general/latest/gr/aws-arns-and-namespaces.html#genref-aws-service-namespaces)\. For example, the `source` value for Amazon CloudFront is `aws.cloudfront`\.

**account**  
The 12\-digit number identifying an AWS account\.

**time**  
The event timestamp, which can be specified by the service originating the event\. If the event spans a time interval, the service might choose to report the start time, so this value can be noticeably before the time the event is actually received\.

**region**  
Identifies the AWS region where the event originated\.

**resources**  
This JSON array contains ARNs that identify resources that are involved in the event\. Inclusion of these ARNs is at the discretion of the service\. For example, Amazon EC2 instance state\-changes include Amazon EC2 instance ARNs, Auto Scaling events include ARNs for both instances and Auto Scaling groups, but API calls with AWS CloudTrail do not include resource ARNs\.

**detail**  
A JSON object, whose content is at the discretion of the service originating the event\. The detail content in the example above is very simple, just two fields\. AWS API call events have detail objects with around 50 fields nested several levels deep\.

To see a list of all event types available from AWS services, see [EventBridge Event Examples from Supported AWS Services](event-types.md)\.