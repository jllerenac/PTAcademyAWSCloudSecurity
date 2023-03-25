# Writable Bucket ACL

Check S3 buckets. `aws s3api list-buckets --profile PTAcademyJllerena`
![image](https://user-images.githubusercontent.com/46797181/227665803-150110cf-9061-4398-a302-72944e5d383e.png)

Check objects present in S3 bucket. `aws s3api list-objects --bucket s3-secret-760068929587 --profile PTAcademyJllerena`

It will give an access denied message. Check the policy `aws s3api get-bucket-acl --bucket s3-secret-760068929587 --profile PTAcademyJllerena`
![image](https://user-images.githubusercontent.com/46797181/227667633-957e2628-5311-412f-a97b-284c84b641a2.png)



























