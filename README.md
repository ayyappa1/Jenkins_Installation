# Install Jenkins on AWS EC2

Jenkins is a self-contained Java-based program, ready to run out-of-the-box, with packages for Windows, Mac OS X and other Unix-like operating systems. As an extensible automation server, Jenkins can be used as a simple CI server or turned into the continuous delivery hub for any project.

# Prerequisites
1.EC2 Instance

    With Internet Access
  
    Security Group with Port 8080 open for internet
    
2. Java v1.8.x

# Install Java

1. We will be using open java for our demo, Get the latest version from http://openjdk.java.net/install/

        yum install java-1.8*

        #yum -y install java-1.8.0-openjdk
    
2. Confirm Java Version and set the java home

        java -version

        find /usr/lib/jvm/java-1.8* | head -n 3

        JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.212.b04-1.el8_0.x86_64

        export JAVA_HOME

        PATH=$PATH:$JAVA_HOME
       //To set it permanently update your .bash_profile
       vi ~/.bash_profile
       
#  Install Jenkins
You can install jenkins using the rpm or by setting up the repo. We will set up the repo so that we can update it easily in the future.

1.Get the latest version of jenkins from https://pkg.jenkins.io/redhat-stable/ and install

    yum -y install wget
    sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
    sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
    yum -y install jenkins
    
  #  Start Jenkins
    // Start jenkins service
    service jenkins start
    //Setup Jenkins to start at boot,
    chkconfig jenkins on
    
  #  Accessing Jenkins
  
      By default jenkins runs at port 8080, You can access jenkins at

      http://YOUR-SERVER-PUBLIC-IP:8080
    
#  Configure Jenkins

1.The default Username is admin

2.Grab the default password

3.Password Location:/var/lib/jenkins/secrets/initialAdminPassword

4.Skip Plugin Installation; We can do it later

5.Change admin password

Admin > Configure > Password

6.Configure java path

Manage Jenkins > Global Tool Configuration > JDK

7.Create another admin user id

#  Test Jenkins Jobs
    1.Create “new item”
    2.Enter an item name – My-First-Project
       Chose Freestyle project
    3.Under the Build section Execute shell: echo "Welcome to Jenkins Demo"
    4.Save your job
    5.Build job
    6.Check "console output"
      
