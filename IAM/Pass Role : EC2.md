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

The student user can run EC2 instances and pass a role to the EC2 instance. Since the student user also has permission to interact with the SSM service, the student user can execute commands on the EC2 instances via SSM. List role on AWS account which can be passed to EC2 service. `aws iam list-roles --profile PTAcademyJllerena` 

![image](https://user-images.githubusercontent.com/46797181/222875518-d3d8cd2b-989d-4717-8ad9-9d44a9b4531c.png)

Check ec2admin role policies and permissions. `aws iam list-role-policies --role-name ec2admin --profile PTAcademyJllerena`
![image](https://user-images.githubusercontent.com/46797181/222875564-89c4e963-4626-46d8-b02a-b2d279a2c073.png)

Check policy permissions. `aws iam get-role-policy --role-name ec2admin --policy-name terraform-20230304040647411800000003 --profile PTAcademyJllerena` 
![image](https://user-images.githubusercontent.com/46797181/222875825-abad55e4-4966-4574-918e-90584843e934.png)

Find AMI id for Amazon Linux 2 AMI. `aws ec2 describe-images --owners amazon --filters 'Name=name,Values=amzn-ami-hvm-*-x86_64-gp2' 'Name=state,Values=available' --output json --profile PTAcademyJllerena | jq -r '.Images | sort_by(.CreationDate) | last(.[]).ImageId'`

The value obtained is `ami-07bf5557ac8caacca`
![image](https://user-images.githubusercontent.com/46797181/222876826-128122a8-3573-40ee-be28-0ba117df9acc.png)

Check the subnets available in the AWS account `aws ec2 describe-subnets --profile PTAcademyJllerena`
![image](https://user-images.githubusercontent.com/46797181/222877273-1e36b971-e35a-43c2-8a7f-01c189a9be89.png)



















