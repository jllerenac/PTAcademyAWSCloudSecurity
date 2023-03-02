### IAM-Cross-Account-Enumeration.md

## Important Note

This exercise was performed with following consideration as terms and conditions from PT Academy

```
EC2 Usage Limits:
t2.micro is allowed in the instance type
The maximum allowed EBS volume size is 16 GB
The maximum allowed EBS IOPS size is 150
Total running instance at any time must not exceed the count of 5
Total instances launched during a lab session must not exceed the count of 10

S3 Usage Limits:
Total S3 bucket at any time must not exceed the count of 5
The total size of a bucket must not exceed 512 MB
The number of objects in a bucket must not exceed the count of 10000

DynamoDB Usage Limits:
Total tables at any time must not exceed the count of 5
The maximum allowed Write Capacity Units is 5
The maximum allowed Read Capacity Units is 5
On-demand DynamoDB tables are not allowed, only provisioned DynamoDB table must be created

Lambda Usage Limits:
The lambda functions at any time must not exceed the count of 5
The maximum allowed memory for a lambda function is 256 MB
The maximum allowed timeout of a lambda function is 120 seconds (2 Minutes)

```

First step is to configure the credentials with `aws configure --profile <name>`

Then, create a `JSON` file with the following content:

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
      "AWS": "*"
    },
      "Action": "sts:AssumeRole",
    "Condition": {}
    }
  ]
}
```
Create a role on the AWS account using AWS CLI using the forged policy. `aws iam create-role --role-name jllRole --assume-role-policy-document file://jllAssumeRole.json --profile PTAcademyJllerena`

![image](https://user-images.githubusercontent.com/46797181/222337466-6cbaef93-f03c-4454-bfa8-621e4a0f5a10.png)

Next step is to use the tool PACU https://github.com/RhinoSecurityLabs/pacu and follow the instructions to install. In my case I installed with `pip3 install pacu`

Then, run pacu and set the PT Academy credentials with `set_keys`
![image](https://user-images.githubusercontent.com/46797181/222338074-b9c84be8-efba-457e-abd2-199a877cd9dc.png)

To list PACU modules run `list`
![image](https://user-images.githubusercontent.com/46797181/222340458-606f8463-b03d-4fdf-b5fd-2b63a575a694.png)

As mentioned in the description, download the names wordlist `wget https://raw.githubusercontent.com/jeswinMathai/wordlist/main/names.txt`
Lets append `-ad` with 

```
#Linux
sed -i 's/^/ad-/g' names.txt    
#Mac OS
sed -i '' 's/^/ad-/g' names.txt

```
![image](https://user-images.githubusercontent.com/46797181/222341732-12f7feb6-4beb-45b3-9f71-4bedfd70baed.png)

Run the pacu module to enumerate roles `run iam__enum_roles --role-name jllRole  --account-id 276384657722 --word-list names.txt` 

Our profile is from a different account and we are able to enumerate another account which is 276384657722 

![image](https://user-images.githubusercontent.com/46797181/222343186-2f1077cb-c852-4ada-a88f-dd42dde03a6a.png)

For users, execute `run iam__enum_users --role-name jllRole  --account-id 276384657722 --word-list names.txt` 

![image](https://user-images.githubusercontent.com/46797181/222344831-2eb980b3-8ad2-4e86-82e3-a4df0690c9e5.png)
