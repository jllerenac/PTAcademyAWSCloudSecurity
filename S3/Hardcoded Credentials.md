# Hardcoded Credentials

After configuring the credentials, list the buckets with `aws s3api list-buckets --profile PTAcademyJllerena`
![image](https://user-images.githubusercontent.com/46797181/227101921-46f32b1e-f0cf-45bc-b801-761dd36ad140.png)

Check bucket objects.

```
aws s3api list-objects --bucket flag-498701622957 --profile PTAcademyJllerena
aws s3api list-objects --bucket s3-upload-498701622957 --profile PTAcademyJllerena
```
![image](https://user-images.githubusercontent.com/46797181/227102640-a358e3c7-fb59-4cad-a54f-7f32c569b0ee.png)

If running `aws s3 cp s3://flag-498701622957/FLAG . --profile PTAcademyJllerena` a forbidden message is obtained

Going to URL `https://s3-upload-498701622957.s3.amazonaws.com/index.html` will show a page. 

![image](https://user-images.githubusercontent.com/46797181/227103487-1cf083e0-686d-426f-b1c0-ea27da4a55f7.png)

Checking the page source will show AWS credentials
![image](https://user-images.githubusercontent.com/46797181/227103707-09b66aca-ff3b-4d77-8cfb-f05d5afc8c9e.png)

Configuring a profile with the new credentials will allow to download the flag 

![image](https://user-images.githubusercontent.com/46797181/227104002-4b5fa842-2fdb-431d-a7be-1df3ec5d9669.png)
