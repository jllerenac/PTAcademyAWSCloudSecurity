### Pass Role : Lambda

 List AWS managed policies attached to the user. Also attempt to create a user to verify that a denied message is received 
 
```
aws iam list-attached-user-policies --user-name student --profile PTAcademyJllerena
aws iam list-user-policies --user-name student --profile PTAcademyJllerena
aws iam create-user --user-name Bob --profile PTAcademyJllerena
 
```
![image](https://user-images.githubusercontent.com/46797181/224526113-bcf89a03-6a78-4795-a59c-c3d7cf920327.png)

Check the policy permissions and details.

![image](https://user-images.githubusercontent.com/46797181/224526152-523acc00-e589-41f4-9637-3dd482379a4c.png)


![image](https://user-images.githubusercontent.com/46797181/224526207-53e767a1-e25e-423f-a159-f6cc01938f2a.png)










