### Pass Role : Lambda

 List AWS managed policies attached to the user. Also attempt to create a user to verify that a denied message is received 
 
```
aws iam list-attached-user-policies --user-name student --profile PTAcademyJllerena
aws iam list-user-policies --user-name student --profile PTAcademyJllerena
aws iam create-user --user-name Bob --profile PTAcademyJllerena
 
```
![image](https://user-images.githubusercontent.com/46797181/224526113-bcf89a03-6a78-4795-a59c-c3d7cf920327.png)

Check the policy permissions and details. `aws iam create-user --user-name Bob --profile PTAcademyJllerena`

![image](https://user-images.githubusercontent.com/46797181/224526152-523acc00-e589-41f4-9637-3dd482379a4c.png)

List role on AWS account which can be passed to Lambda. ` aws iam list roles --profile PTAcademyJllerena`
![image](https://user-images.githubusercontent.com/46797181/224526313-aeac9b87-1932-4c6c-aca5-447f66e70c4c.png)
![image](https://user-images.githubusercontent.com/46797181/224526322-2c54aa02-3f2c-43a7-a8aa-040b9913002d.png)
![image](https://user-images.githubusercontent.com/46797181/224526339-9a1115b9-3172-4f20-9a06-bc75059cbd26.png)
![image](https://user-images.githubusercontent.com/46797181/224526347-05c050a9-fd93-4686-9991-38ae997aac92.png)

Check lab11lambdaiam role details.

```
aws iam get-role --role-name lab11lambdaiam --profile PTAcademyJllerena
aws iam list-role-policies --role-name lab11lambdaiam --profile PTAcademyJllerena
aws iam get-role-policy --role-name lab11lambdaiam --policy-name terraform-20230312051026653800000003 --profile PTAcademyJllerena

```
![image](https://user-images.githubusercontent.com/46797181/224526533-14c33639-6075-4046-a576-4e4aad128396.png)

Create a python script with the following content and compress it as zip with `zip aws.zip aws.py`

```
import boto3
def handler(event, context):
 iam = boto3.client("iam")
 response = iam.attach_user_policy(
  UserName="student", PolicyArn="arn:aws:iam::aws:policy/AdministratorAccess"
 )
 return response

```

Create a lambda function on AWS account. `aws lambda create-function --function-name jllerena --runtime python3.8 --zip-file fileb://aws.zip --handler jll.handler --role arn:aws:iam::350092314133:role/lab11lambdaiam --profile PTAcademyJllerena`

![image](https://user-images.githubusercontent.com/46797181/224526732-29b4f14e-3a2b-406d-8178-5deda0458a8c.png)

Invoke the newly created Lambda function `aws lambda invoke --function-name jllerena jllerena_out.txt --profile PTAcademyJllerena`
![image](https://user-images.githubusercontent.com/46797181/224526797-670a745c-fccb-4ef1-a7f3-2050b6daf346.png)

Check attached policies on student user.







