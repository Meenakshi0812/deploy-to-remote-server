### deploy-to-remote-server
## problem statement
- needs to clone the the code in /home/ec2-user/
- and the folder name should be the $build_number
- then we need to zip the all the files
- copy the zip folder to remote server(i.e application-server) in the application folder path i.e /var/www/html
- then unzip the folder in /var/www/html/
- then create the soft link for the updated code with the zipped code
- next expose the application through internet.
- make process as automate whenever new commit triggers buids need to trigger automatically
## solution
- create servers (take any os of ur choice whether linux/ubuntu) .
- name the first server as jenkins-server and install jenkins in it
- name second server as application-server and install apache2 in it
- create a pipeline and create the required stages and steps
- run the pipeline and if it success, the copy the ip address of application-server and expose it internet to check the application is working or not.
- to make automatic create webhooks in git.

## steps to install jenkins in linux
``` 
sudo yum update –y
sudo wget -O /etc/yum.repos.d/jenkins.repo \
    https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
sudo yum upgrade
sudo dnf install java-11-amazon-corretto -y
sudo yum install jenkins -y
sudo systemctl enable jenkins
sudo systemctl start jenkins
sudo systemctl status jenkins
```
- note: dont forgot to enable port 8080 in security groups.
- once installed open the jenkins in browser ip:8080
## steps to install apache2
```
sudo apt update
sudo apt install apache2
sudo systemctl status apache2
```
- once installed copy the ip adrdress of application server and check whetehr apache running or not.
- if u got error like zip not installed like that install zip.
- to install zip in linux use command
```
sudo yum install zip
```
to install zip in ubuntu
```
sudo apt install zip
```
- to use scp command u need to copy the public key (id_rsa.pub) to the authorized_keys file of remote server.
- if u dont have existing ssh keypairs then u can generate by using command
```
ssh-keygen
```
- next ,
- run the pipeline if got any errors resolve those errors once build got suceess check the application-server ip in browser to check whether default index.html page of apache server replaced with index.html page which u created.
