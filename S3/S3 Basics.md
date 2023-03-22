### S3 Basics 

Open the lab link and a web shell will be opened in a new tab
Execute `ip addr` to see the ip address which is `192.232.110.2/24`
![image](https://user-images.githubusercontent.com/46797181/226777666-286fc121-053a-43a1-8b46-8c2eda33d6a1.png)

As indicated in the instructions, IP address of the target machine ends in `.3` which means that the address is `192.232.110.3`
Run `nmap 192.232.110.3` to see the opened ports. As seen below the opened port is `9000`

![image](https://user-images.githubusercontent.com/46797181/226778136-94ac68fc-e577-4f68-8469-dd3e35778983.png)

Running the command `curl 192.232.110.3:9000` will give a denied message in XML format or `curl 192.232.110.3:9000 -s | xmllint --format -` to output in a more friendly format
![image](https://user-images.githubusercontent.com/46797181/226778491-7d75134d-4b12-4380-bace-46b8e94871ec.png)

Output shows that S3 bucket may be running on that ports. Lets configure AWS CLI with `AWS configure` and enter the access keys provided

List the buckets with `aws --endpoint http://192.232.110.3:9000 s3api list-buckets` 
![image](https://user-images.githubusercontent.com/46797181/226779629-1f68b808-84da-4b1d-a05f-cf0edf991d90.png)


