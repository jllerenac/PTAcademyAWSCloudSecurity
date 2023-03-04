### Dangerous Policy Combination II

First the profile has to be configured with the access keys provided by PT Academy

## Walkthrough

Get the attached user policies for `student` user which shows `IAMReadOnlyAccess` permission 

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






