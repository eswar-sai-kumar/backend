# Jenkins

### Create 3 instances
- jenkins
- jenkins-agent
- nexus
  
### Create key-pair

### Create records

All the above resources are created using terraform which is present in **terraform-aws-tools** repository

# 1. Open **jenkins** instance in server and run the below command

```
sh jenkins.sh
```

jenkins.sh is present in **terraform-aws-tools** repository

### Open in browser 

<public_ip_jenkins>:8080 

copy the path 

cat <copy_path> (**copy the password and enter in the jenkins**)


# 2. Open **jenkins-agent** instance in server and run the below command

**(configure aws credentials in jenkins-agent using "aws configure" command, make sure that run in a normal user)**

```
sh jenkins-agent.sh
```

jenkins-agent.sh is also present in **terraform-aws-tools** repository

# 3. Open **nexus** instance in server by following command in bash

ssh -i "c:/repos/key-pair.pub" ubuntu@<public_ip_nexus>

### Open in browser

<public_ip_nexus>:8081

copy path present in the browser

cat <copy_path> (**copy the password and enter in the nexus**)


Nexus → settings → repo → create → maven2 hosted → name(bakend) → version ploicy(mixed) → layout policy(permissiva) → deployment policy (allow redeploy) → create → copy url

Jenkins → Manage jenkins → create node(expense) → remote root(/home/ec2-user/jenkins-agent) → Labels(AGENT-1) → Usage(only build jobs) → launch via ssh → jenkins-agent.eswarsaikumar.site

Jenkins → Expense folder → ok

+New Item → backend → pipeline → scm(git) enter all details of repo → apply → save

+New Item → backend-deploy → pipeline → scm(git) enter all details of repo → apply → save

How to move zip file to nexus (have to install **nexus artifact downloader**(plugin) in jenkins)

**adding nexus credentials in jenkins** Jenkins → credentials → global → add → username > password → id(nexus-auth) → add

Run the backend pipeline, we can see zip file will get downloaded in nexus




