# Chaining Attacks

Check S3 buckets. `aws s3api list-buckets --profile PTAcademyJllerena`
![image](https://user-images.githubusercontent.com/46797181/227757045-5fe0977c-58a0-48a8-9d50-a79da3574459.png)

List bucket contents. 

```
aws s3 ls s3://s3-file-load-845168849788 --profile PTAcademyJllerena
aws s3 ls s3://s3-file-load-static-845168849788 --profile PTAcademyJllerena

```
![image](https://user-images.githubusercontent.com/46797181/227757255-998e4eb3-6d8d-4cb8-814f-cb47e9eda231.png)

Check if a static website is available in the browser. Enter the URL in the format `http://s3-file-load-402113608956.s3-website-us-east-1.amazonaws.com/`
![image](https://user-images.githubusercontent.com/46797181/227757843-44100fd9-3cee-4c79-b513-016096a64dcd.png)

Checking the source code, it is possible to see that the application points to the other bucket
![image](https://user-images.githubusercontent.com/46797181/227757961-974638a6-fb24-4383-adf1-7afae792ad0a.png)

Checking the other bucket `aws s3 ls s3://s3-file-load-static-402113608956/static/ --profile PTAcademyJllerena` it can be seen that there are files in there 
![image](https://user-images.githubusercontent.com/46797181/227758067-4e6f663f-ae64-45c8-ae29-ca22b0f3e0e8.png)

Check the bucket policy `aws s3api get-bucket-policy --bucket s3-file-load-static-402113608956 --output text  --profile PTAcademyJllerena | jq `
![image](https://user-images.githubusercontent.com/46797181/227758140-4c74218c-a0c4-42ae-a4fa-8ba11114025b.png)


