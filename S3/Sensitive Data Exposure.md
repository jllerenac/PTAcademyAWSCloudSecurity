# Sensitive Data Exposure

Go to URL `https://uyphi3oonj.execute-api.ap-southeast-1.amazonaws.com/default`

![image](https://user-images.githubusercontent.com/46797181/226799555-ac06cb10-dcfb-4128-b109-fc9ee890db77.png)

Right click on the page and select `view source code`, notice that there are URL pointing to an AWS URL
![image](https://user-images.githubusercontent.com/46797181/226799993-13afd284-8ddc-4eac-a39b-3cbd3e30904e.png)

Going to the URL will list a bucket
![image](https://user-images.githubusercontent.com/46797181/226800063-ee259378-63ce-4037-a425-45c26fb534e7.png)

Copy the bucket name and enumerate bucket using AWS CLI.
Check the objects of the bucket in the scripts directory.
Download backup.sh object from the bucket.
Check the downloaded script.

```
aws s3 --no-sign-request --region ap-southeast-1 ls s3://lab-webapp-static-resources
aws s3 --no-sign-request --region ap-southeast-1 ls s3://lab-webapp-static-resources/scripts/
aws s3 --no-sign-request --region ap-southeast-1 cp s3://lab-webapp-static-resources/scripts/backup.sh ./
cat backup.sh 

```
![image](https://user-images.githubusercontent.com/46797181/226801022-c4d91a39-07c9-4f3d-8a4c-4c52c4ef09ad.png)

The backup file shows a curl command with API key and outputs to a file, running the command and opening the file will give a list of users and passwords along with the flag

![image](https://user-images.githubusercontent.com/46797181/226802025-ffddc380-bf6c-4d96-a243-ef91e522b2c1.png)


EXERCISE COMPLETED







