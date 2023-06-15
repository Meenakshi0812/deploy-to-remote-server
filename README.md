# deploy-to-remote-server
## problem statements
- needs to clone the the code in /home/ec2-user/
- and the folder name should be the $build_number
- then we need to zip the all the files
- copy the zip folder to remote server(i.e application-server) in the application folder path i.e /var/www/html
- then unzip the folder in /var/www/html/
- then create the soft link for the updated code with the zipped code
- next expose the application through internet.
- make process as automate whenever new commit triggers buids need to trigger automatically
## solutions
- create servers (take any os of ur choice whether linux/ubuntu) .
- name the first server as jenkins-server and install jenkins in it
- name second server as application-server and install apache2 in it
- create a pipeline and create the required stages and steps
- run the pipeline and if it success, the copy the ip address of application-server and expose it internet to check the application is working or not.
- to make automatic create webhooks in git.

## steps to install jenkins in linux
- <sudo yum update –y>
- <sudo wget -O /etc/yum.repos.d/jenkins.repo \
    https://pkg.jenkins.io/redhat-stable/jenkins.repo>
- <sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key>
- <sudo yum upgrade>
- <sudo dnf install java-11-amazon-corretto -y>
- < sudo yum install jenkins -y>
- <sudo systemctl enable jenkins>
- <sudo systemctl start jenkins>
- <sudo systemctl status jenkins>
- [OpenAI](https://openai.com)
