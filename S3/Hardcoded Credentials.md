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
