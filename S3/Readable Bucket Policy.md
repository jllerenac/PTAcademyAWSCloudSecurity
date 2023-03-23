# Readable Bucket Policy

Check the S3 buckets with `aws s3api list-buckets --profile PTAcademyJllerena`

Check objects present in S3 bucket. `aws s3api list-objects --bucket s3-readable-policy-352839283984 --profile PTAcademyJllerena`
![image](https://user-images.githubusercontent.com/46797181/227366308-c050a7cc-3e3a-4d20-9857-d453de9296ae.png)

As seen above, listing the object is not possible due to insufficient permissions.

Check bucket policy. `aws s3api get-bucket-policy --bucket s3-readable-policy-352839283984 --output text --profile PTAcademyJllerena`


