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





