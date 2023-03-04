### Overly Permissive Permission II 

After configuring the credentials, get details of current user `aws iam get-user --profile PTAcademyJllerena`

![image](https://user-images.githubusercontent.com/46797181/222873474-b688b6ca-7998-4409-b87a-415b23b52130.png)

Get information about the policies attached to the user. 

```
aws iam list-user-policies --user-name student --profile PTAcademyJllerena
aws iam get-user-policy --user-name student --policy-name terraform-20230304031918444600000001 --profile PTAcademyJllerena

```
![image](https://user-images.githubusercontent.com/46797181/222873598-2e010af4-75d2-470d-a91d-c6aa48de540e.png)

The user has permission to create a login profile for any user. Check for users with “AdministratorAccess” policy attached to them.

```
aws iam list-users --profile PTAcademyJllerena
aws iam list-attached-user-policies --user-name Admin[Jane|Bob] --profile PTAcademyJllerena

```
![image](https://user-images.githubusercontent.com/46797181/222874171-39c5de5e-636c-4e21-b3e9-a08390c3ab9d.png)

Both users Bob and Jane have administrator access 

![image](https://user-images.githubusercontent.com/46797181/222874250-28dbfebc-32b7-4385-a6ab-42899b687526.png)

Create a login profile for user AdminBob. `aws iam create-login-profile --user-name AdminBob --password Bobby11@ --no-password-reset-required --profile PTAcademyJllerena`

![image](https://user-images.githubusercontent.com/46797181/222874448-1dd6a781-d65f-4d58-9387-ebf33fa425a1.png)

Log in AWS console with the credentials created 
![image](https://user-images.githubusercontent.com/46797181/222874481-660f2b92-768b-4ae5-bfef-6df1eafc5385.png)

Admin access has been obtained 
![image](https://user-images.githubusercontent.com/46797181/222874645-747bdd11-378b-45ee-a8b5-d2a805ddafd2.png)















