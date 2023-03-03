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
