---
title: 'AWS - Checking out logs the devops way'
category: 'aws'
coverImage: '/assets/blog/dynamic-routing/cover.jpg'
date: '2020-03-16T05:35:07.322Z'
author:
  name: Nahuel Chaves
  picture: '/assets/blog/authors/nahuel.jpeg'
ogImage:
  url: '/assets/blog/dynamic-routing/cover.jpg'
---

I would like to tell you about a package i use a lot for checking out logs, let's make something clear, the cloudwatch UI is not very helpful for looking through logs searching for a error log.

This package is called [awslogs](https://github.com/jorgebastida/awslogs), and you can install it very easily. Just type `pip install awslogs` and hit enter.

The only requirement is to have configured a IAM user with the following policy document:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Action": [
                "logs:Describe*",
                "logs:Get*",
                "logs:List*",
                "logs:TestMetricFilter",
                "logs:FilterLogEvents"
            ],
            "Effect": "Allow",
            "Resource": "*"
        }
    ]
}
```

And then is really simple.. just type something like `awslogs get <loggroup> <stream>`

For example let's say you have a log group called `app_logs` and a stream called `production/gateway`.

You would have to run `awslogs get app_logs production/gateway`. Easy huh?. You will have a beautiful and easy to read output.

There's ton of parameters you can set to filter out the output, but i will leave you to check their website.

And remember, as this is a open source project, please support them in any way you can.