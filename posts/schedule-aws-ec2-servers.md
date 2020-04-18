---
title: "AWS - Schedule EC2 Shutdown and Startup"
excerpt: "This way we dont pay unused hours"
category: 'aws'
coverImage: '/assets/blog/dynamic-routing/cover.jpg'
date: '2020-03-16T05:35:07.322Z'
author:
  name: Nahuel Chaves
  picture: '/assets/blog/authors/nahuel.jpeg'
cover: ec2.png
ogImage:
  url: '/assets/blog/dynamic-routing/cover.jpg'
---

Go to the AWS dashboard, and enter the IAM module. Then you need to create the following policy under the name `ec2_start_stop_policy`.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "Stmt1444812758000",
            "Effect": "Allow",
            "Action": [
                "ec2:DescribeInstanceStatus",
                "ec2:DescribeInstances",
                "ec2:StartInstances",
                "ec2:StopInstances"
            ],
            "Resource": [
                "*"
            ]
        },
        {
            "Action": [
                "logs:CreateLogGroup",
                "logs:CreateLogStream",
                "logs:PutLogEvents"
            ],
            "Effect": "Allow",
            "Resource": "arn:aws:logs:*:*:*"
        }
    ]
}
```

Then create a IAM Role called `ec2_start_stop_role`, that uses Lambda as a service, and assign the created policy.

Create 2 lambda functions `start-server` and `stop-server`, with the following configuration:

* `Role`: `ec2_start_stop_role`
* `Memory`: `128MB`
* `Timeout`: `59s`

In the code editor, enter the following content:


```
import boto3
# Enter the region your instances are in. Include only the region without specifying Availability Zone; e.g., 'us-east-1'
region = 'XX-XXXXX-X'
# Enter your instances here: ex. ['X-XXXXXXXX', 'X-XXXXXXXX']
instances = ['X-XXXXXXXX']

def lambda_handler(event, context):
    ec2 = boto3.client('ec2', region_name=region)
    ec2.stop_instances(InstanceIds=instances)
    print 'stopped your instances: ' + str(instances)
```

Change `stop_instances` with `start_instances` on the `start-server` lambda.


## Create a CloudWatch Event that triggers your Lambda function at night

* Add a trigger, select CloudWatch Events as a source.
* Create a new rule, and enter something like `cron(0 1 * * ? *)` in the expression. That means that it will run every day at 1AM.

* Hit Save.

## Create a CloudWatch Event that triggers your Lambda function in the morning

* Add a trigger, select CloudWatch Events as a source.
* Create a new rule, and enter something like `cron(0 8 * * ? *)` in the expression. That means that it will run every day at 8AM.

* Hit Save.