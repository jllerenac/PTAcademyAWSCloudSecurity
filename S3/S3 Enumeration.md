### S3 Enumeration 

## Console S3 Enumeration

Log in the console and click on `S3` link or search for S3 dashboard
![image](https://user-images.githubusercontent.com/46797181/224888763-9c03d668-5283-4f88-b2ba-c92d3086893e.png)

In the dashboard there will be a list of all the buckets
![image](https://user-images.githubusercontent.com/46797181/224888911-7e678db6-aba4-4116-a222-a47d3f4b7b28.png)

Click on one of the buckets to see its objects.
![image](https://user-images.githubusercontent.com/46797181/224889008-190fcf7b-40d5-40ea-b0c9-2eef47aff05e.png)

Click on `properties` tab to see its properties.
![image](https://user-images.githubusercontent.com/46797181/224889146-7f2f5271-1a5f-43a0-baa3-f592df7e3da9.png)

As seen in above image, bucket versioning is enabled. Go back to `objects` properties and enable `show versions`
![image](https://user-images.githubusercontent.com/46797181/224889384-2a109f68-eb00-450d-8ec6-5a125906d102.png)

Click on the version to see its details
![image](https://user-images.githubusercontent.com/46797181/224890045-669ed9b4-ff29-443b-b52e-20ba102d4945.png)

Download and open the file, a lambda function is shown
![image](https://user-images.githubusercontent.com/46797181/224890290-940e3ba9-2d80-44b6-96a7-fc7838bfd78c.png)

Now, check the bucket permission which can be seen that is not public
![image](https://user-images.githubusercontent.com/46797181/224890803-b907c97c-7cfb-4260-9a76-3c59b90d411d.png)

Go to ‘Access Points’ tab to check the named network endpoints attached to the bucket.
![image](https://user-images.githubusercontent.com/46797181/224891077-479edfe1-0793-4dbe-8b82-2398f68f6c11.png)

Perform similar check on other buckets, focus on finding publicly accessibles buckets
![image](https://user-images.githubusercontent.com/46797181/224891588-6e854e4f-349d-40d6-bc0d-602774917cb2.png)

Go to storage lens dashboard and click on the dashboard to view its details
![image](https://user-images.githubusercontent.com/46797181/224891779-a9b62a0f-3311-4d8f-85bc-edb6f39aa880.png)

![image](https://user-images.githubusercontent.com/46797181/224892078-523b354a-39ba-44ac-9929-e240b25b3308.png)

## AWS CLI S3 BUCKET ENUMERATION

First lets configure the access keys with `aws configure --profile --profile PTAcademyJllerena`


















