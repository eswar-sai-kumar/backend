# Jenkins

### Create 3 instances
- jenkins ()
- jenkins-agent
- nexus
  
### Create key-pair

### Create records

All the above resources are created using terraform which is present in **terraform-aws-tools** repository

### Open **jenkins** instance in server and run the below command

```
sh jenkins.sh
```

jenkins.sh is present in **terraform-aws-tools** repository

### Open **jenkins-agent** instance in server and run the below command

```
sh jenkins-agent.sh
```

jenkins-agent.sh is also present in **terraform-aws-tools** repository

### Open **nexus** instance in server


### Open in browser 

<public_ip_jenkins>:8080 
copy the path 
cat <copy_path> (**copy the password and enter in the jenkins**)
**(configure aws credentials in jenkins)**


<public_ip_nexus>:8081





