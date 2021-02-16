---
published: true
title: AWS Cross Account Access
---
It's all about trust.

## A Tale of Two Accounts

Recently I had need of accessing staging resources from my development account. As this was not something I do regularly, it's probably a good idea to document it.

### Staging Account Configuration

My need was full access to staging S3 buckets, so I create a role named "role-staging-s3" with the following policy:

	{
    	"Version": "2012-10-17",
		"Statement": [
			{
				"Effect": "Allow",
				"Action": "s3:*",
				"Resource": "*"
			}
		]
	}


To keep things simple, I've left access pretty wide open. More fine-grained permissions are left as an exercise for the reader.

Under the "Trust relationships" tab, I add the following policy:
```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::<DEVELOPMENT_ACCOUNT>:root"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
```

### Development Account Configuration

On the development account, I created a group called "group-staging-s3" with the following policy:

```
{
  "Version": "2012-10-17",
  "Statement": {
    "Effect": "Allow",
    "Action": "sts:AssumeRole",
    "Resource": "arn:aws:iam::<STAGING_ACCOUNT>:role/role-staging-s3"
  }
}
```

I then added any user I want to grant access to staging buckets to the group.

### Local Configuration

We'll need to set up a profile to use the new role in `~/.aws/config`:

```
[profile dev-user]
region=<SOME_AWS_REGION>
aws_account=<DEVELOPMENT_ACCOUNT>

[profile staging-s3]
source_profile=dev-user
region=<SOME_AWS_REGION>
role_arn=arn:aws:iam::<STAGING_ACCOUNT>:role/staging-s3-role
```

Remember to configure access in `~/.aws/credentials`:

```
[dev-user]
aws_access_key_id=<DEV_USER_AWS_ACCESS_KEY>
aws_secret_access_key=<DEV_USER_AWS_ACCESS_SECRET>
```

### Test access

```
aws --profile staging-s3 s3 ls
```

All buckets should be listed since we allowed all S3 permissions.
