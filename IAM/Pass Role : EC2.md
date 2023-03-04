### Pass Role : EC2

Configure the profile with the credentials provided. Then, list the policies attached to the user. Also, list inline policies attached to the user.

```
aws iam list-attached-user-policies --user-name student --profile PTAcademyJllerena
aws iam list-user-policies --user-name student --profile PTAcademyJllerena

```

![image](https://user-images.githubusercontent.com/46797181/222875109-e7bdae68-e3f5-4287-aeb7-507b8bc83216.png)


Attempt to create a user on the AWS account. `aws iam create-user --user-name jllerena --profile PTAcademyJllerena` A denied message is received 
![image](https://user-images.githubusercontent.com/46797181/222875129-893f9c02-3e0e-4f23-8ae6-b10c9f482c7e.png)

Check the policy permissions and details. `aws iam get-user-policy --user-name student --policy-name ConfigureEC2Role --profile PTAcademyJllerena` 
![image](https://user-images.githubusercontent.com/46797181/222875168-43144363-8658-4f2a-80c7-4bd2e3fd6484.png)























