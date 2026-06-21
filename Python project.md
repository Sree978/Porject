STages

<img width="1128" height="281" alt="image" src="https://github.com/user-attachments/assets/2ac28fe1-0ce3-4507-b551-9f721d73def9" />


Take m7i-flex server 2  ( one for jenkins one for manager )
t3 micro servers 2 ( workers) 

Jenkins server  ---> install jenkins 
Manager server  ---> install docker & install compose & docker swarm and copy to key every worker node ( create cluster  ) + install git also + install java 
W1 & w2  & jenkins also --> install docker

Create connection b/w manager and jenkins server 

Manage jenkins > setup agent > node name : managernode enable perminent agent + create 
no of executers  : 2 , remote root directory : /home/ec2-user/jenkins  , label : prod
usage: only build jobs with label expressions matching this node 
launch method : via ssh 
host : manager server ip 54.167.60.138
credentails : ssh username with private key   
hostkey verification strategy : Non verifying verification startegy 

Create a job over jenkins 








