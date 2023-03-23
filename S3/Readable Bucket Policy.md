# Readable Bucket Policy

Check the S3 buckets with `aws s3api list-buckets --profile PTAcademyJllerena`

Check objects present in S3 bucket. `aws s3api list-objects --bucket s3-readable-policy-352839283984 --profile PTAcademyJllerena`
![image](https://user-images.githubusercontent.com/46797181/227366308-c050a7cc-3e3a-4d20-9857-d453de9296ae.png)

As seen above, listing the object is not possible due to insufficient permissions.

Check bucket policy. `aws s3api get-bucket-policy --bucket s3-readable-policy-352839283984 --output text --profile PTAcademyJllerena | jq` Instead of `jq` it can use `python3 -m json.tool` 
![image](https://user-images.githubusercontent.com/46797181/227367794-af131523-8652-4408-b7b3-ddc278af206f.png)

According to the above permission it is possible to get object (`s3:GetObject`) on `"arn:aws:s3:::s3-readable-policy-352839283984/this-is-flag` which means that the resource is showing the object name `this-is-flag`

Simpley copy the file and show `aws s3 cp s3://s3-readable-policy-352839283984/this-is-flag ./ --profile PTAcademyJllerena`

![image](https://user-images.githubusercontent.com/46797181/227369412-a1e3d719-13a1-4afa-8180-21550973851b.png)

EXERCISE COMPLETED 
