
### IAM ENUMERATION

## Console Enumeration

We go to the link provided by PT Academy when starting the lab 

![image](https://user-images.githubusercontent.com/46797181/222305461-92c6103b-7fd2-4557-b2a1-fba4afc3657c.png)

We enter the credentials provided to log in the console, then we go to IAM and click on users

![image](https://user-images.githubusercontent.com/46797181/222305911-211d23db-6fab-482f-a87d-2806eab1ca7a.png)

To enumerate a user we click on a user and explore the different tabs

![image](https://user-images.githubusercontent.com/46797181/222306135-e811b5f1-b284-42c8-903d-dca7ef2ed622.png)
![image](https://user-images.githubusercontent.com/46797181/222306169-315f1edb-5e22-443e-8a18-9716a26dd369.png)
![image](https://user-images.githubusercontent.com/46797181/222306289-649f2c0b-9812-4c0e-8111-784e5d07d6cb.png)
![image](https://user-images.githubusercontent.com/46797181/222306308-2cb9afb4-cdf3-49a4-8a4a-9d185a5f2594.png)
![image](https://user-images.githubusercontent.com/46797181/222306346-0d9e3cc9-3c58-422d-b0dc-68336f76c6ea.png)

We can keep exploring other users and check the security credentials to see if something can be found like any access key or SSH keys
![image](https://user-images.githubusercontent.com/46797181/222307055-e644b9f2-b78b-41db-a1c3-c27a22b5359d.png)

Policies can also be checked
![image](https://user-images.githubusercontent.com/46797181/222307266-558b2985-aff4-4731-808c-d1c15883ea90.png)

Groups can also be enumerated as well

![image](https://user-images.githubusercontent.com/46797181/222307487-bad77e27-aa2f-407b-bef8-9af13a119341.png)

Role enumeration to see permissions and trust relationships
![image](https://user-images.githubusercontent.com/46797181/222308959-f7fe6791-3c8d-499c-88aa-ae5c2a046d45.png)
![image](https://user-images.githubusercontent.com/46797181/222309018-9c17c2a4-8761-4bb5-ab9b-b80aff991f2a.png)

Click on the policy to see its information
![image](https://user-images.githubusercontent.com/46797181/222309188-dc71104e-d8f8-4cc7-b5c8-1e6c9ded4ca5.png)

## AWS CLI enumeration 
First configure the profile with the access keys provided with `aws configure --profile PTAcademyJllerena`
![image](https://user-images.githubusercontent.com/46797181/222309574-1c5a6164-bca7-4e53-a89b-c20dbb2221bb.png)

To enumerate users execute `aws iam list-users --profile PTAcademyJllerena`
![image](https://user-images.githubusercontent.com/46797181/222309784-414250dd-6f72-42e2-8628-d71cf1218302.png)

To list groups for a user execute `aws iam list-groups-for-user --user-name ad-adminson --profile PTAcademyJllerena`
![image](https://user-images.githubusercontent.com/46797181/222310570-e5c69dc5-1e86-40a9-b3b7-8a5cdf0f30fa.png)

To list policies for user execute `aws iam list-attached-user-policies --user-name ad-adminson --profile PTAcademyJllerena`
![image](https://user-images.githubusercontent.com/46797181/222310891-a9ade260-d59f-4fcf-8370-1acfab2c0c77.png)

To check a signing certificate for a user execute `aws iam list-signing-certificates --user-name ad-user --profile PTAcademyJllerena`
![image](https://user-images.githubusercontent.com/46797181/222311125-26b127b1-b879-4b32-9f1d-a24e27d9cc4b.png)

To check any ssh public key, execute `aws iam list-ssh-public-keys --user-name ad-user --profile PTAcademyJllerena`
![image](https://user-images.githubusercontent.com/46797181/222311542-a050d8a5-92a5-4225-ae27-a8f159070468.png)

Get the ssh key details with `aws iam get-ssh-public-key --user-name ad-user --encoding PEM --ssh-public-key-id APKAUAWOPGE5M47NZEIT --profile PTAcademyJllerena`
![image](https://user-images.githubusercontent.com/46797181/222312198-4525a9b4-9e3a-4fbc-8784-3d7e0f780ddf.png)

Check for MFA devices for users by executing `aws iam list-virtual-mfa-devices --profile PTAcademyJllerena` 
![image](https://user-images.githubusercontent.com/46797181/222312537-326d079e-2330-4c95-b032-718a9a293e6f.png)

Check for user login profile with `aws iam get-login-profile --user-name ad-user --profile PTAcademyJllerena`
![image](https://user-images.githubusercontent.com/46797181/222312980-217d80e9-c7d7-4b29-881c-5eea97f1e2a0.png)

