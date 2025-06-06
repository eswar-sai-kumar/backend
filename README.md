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

- <public_ip_jenkins>:8080 

copy the path 

- cat <copy_path> (**copy the password and enter in the jenkins**)


# 2. Open **jenkins-agent** instance in server and run the below command

**(configure aws credentials in jenkins-agent using "aws configure" command, make sure that run in a normal user)**

```
sh jenkins-agent.sh
```

jenkins-agent.sh is also present in **terraform-aws-tools** repository

# 3. Nexus 

Open nexus instance in server by following command in bash

- ssh -i "c:/repos/key-pair.pub" ubuntu@<public_ip_nexus>

### Open in browser

- <public_ip_nexus>:8081

copy path present in the browser

- cat <copy_path> (**copy the password and enter in the nexus**)


- Nexus → settings → repo → create → maven2 hosted → name(backend) → version ploicy(mixed) → layout policy(permissiva) → deployment policy (allow redeploy) → create → copy url

- Jenkins → Manage jenkins → create node(expense) → remote root(/home/ec2-user/jenkins-agent) → Labels(AGENT-1) → Usage(only build jobs) → launch via ssh → jenkins-agent.eswarsaikumar.site

- Jenkins → Expense folder → ok

- +New Item → backend → pipeline → scm(git) enter all details of repo → apply → save

- +New Item → backend-deploy → pipeline → scm(git) enter all details of repo → apply → save

- How to move zip file to nexus (have to install **nexus artifact downloader**(plugin) in jenkins)

- **adding nexus credentials in jenkins** Jenkins → credentials → global → add → username → password → id(nexus-auth) → add

- Nexus → settings → repo → create → maven2 hosted → name(frontend) → version ploicy(mixed) → layout policy(permissiva) → deployment policy (allow redeploy) → create → copy url


Run the backend pipeline, we can see zip file will get downloaded in nexus

# 4. SonarQube (port number : 9000)

- Create EC2 instance (t3.medium, AMI: SonarQube CE on AWS, keypair: key-pair, config storage: 1*30 GiB)

- Open on browser (ip:9000) → Username → password (sonarqube instance id) → create password 

- Jenkins → plugins → install sonar qube scanner

- Jenkins → manage jenkins → tools → sonarqube scanner installations > Name : sonar → tick Install automatically → save

- Manage jenkins → system → sonarqubse servers → tick env variables → add → name: sonar-6.0 → server url: https://<ip>:9000/ → save

- SonarQube → myaccount → security → name: jenkins → type: global analysis token → Expiration: No expiration → Generate → copy

- Jenkins → Manage jenkins → credentials → system → global credentials → add → kind: secret text → secret: enter the copied secret → ID: sonar-auth → Desc: sonar-auth → Create

- Manage jenkins → System → sonar auth token: sonar-auth → apply → save

After completion of deploying

- SonarQube → Projects → We can see the status

- SonarQube → Quality gates → Create → Can see conditions here → Can edit anything (on "New code" or on "Overall code" like coverage, critical issues, security rating, vulnerabilities etc) 

- SonarQube → Administration → Configuration → Webhook → Create → Name: jenkins → Url: https://jenkins.eswarsaikumar.site:/8080/sonarqube-webhook/

- GitHub repo → security → code scanning → configure scanning tool → code scanning → tools → codeQL analysis → Set up: default

Github will scan continuously

DAST: ()

- Browser → Veracode → add target → web appn → next → target name: expense → url: web-cdn.eswarsaikumar.site → default team → next → quick scan → create target → run analysis



