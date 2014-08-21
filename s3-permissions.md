#S3 Permissions
In order to use Harpoon with S3, you'll want to create a restricted IAM user that has access only to S3 and Route 53.

When you create the user, make sure you save the users Access key and Secret token for later.  Harpoon will ask for it the first time it's run.

Here are the permissions the user will need:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:*",
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": [
        "route53:*"
      ],
      "Resource": [
        "*"
      ]
    }
  ]
}
```
