### Pass Role : CloudFormation

List AWS managed policies attached to the user and try to create a user.
```

aws iam list-attached-user-policies --user-name student --profile PTAcademyJllerena
aws iam list-user-policies --user-name student --profile PTAcademyJllerena
aws iam create-user --user-name Bob --profile PTAcademyJllerena

```

Check the policy permissions and details. `aws iam get-user-policy --user-name student --policy-name terraform-20230312061123165200000001 --profile PTAcademyJllerena`

![image](https://user-images.githubusercontent.com/46797181/224528133-2890d298-7c22-4515-9da6-88601bb81feb.png)

List role on AWS account which can be passed to CloudFormation service `aws iam list-roles --profile PTAcademyJllerena`
![image](https://user-images.githubusercontent.com/46797181/224528240-63cd8c63-2790-4d56-bd90-5da567ac4805.png)
![image](https://user-images.githubusercontent.com/46797181/224528273-bc25821f-d474-46a5-800a-f23c3d3b6c07.png)

