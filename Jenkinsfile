pipeline
{
  
agent 
{
label "UnixSlave"

}
  

  environment {
    registry = "shanmukha511/tomcat"
    registryCredential = 'DockerHubCred'
}
  

parameters
{
 choice(name: 'Environment',choices: 'Dev\nUAT\nPRD',description: 'Please select Environment')
 string(name:  'servername',description: 'Please enter ip address of Machine where you want to deploy artifact')
 string(name:  'Jobname',description: 'Please Jobname to get ocation of artifact')
 
 
}

stages
{
stage("build")
{

 steps{

 sh "mvn clean package"
  
 //sh "scp -v -o StrictHostKeyChecking=no /tmp/workspace/${params.Jobname}/target/biomni-1.0-SNAPSHOT.jar root@${params.servername}:/tmp"
  //sh "ssh -tt -v -o StrictHostKeyChecking=no root@${params.servername} 'docker cp /tmp/biomni-1.0-SNAPSHOT.jar ${params.ContainerId}:/usr/local/tomcat/webapps'"
  //def ret = sh(script: 'uname', returnStdout: true)
  //println ret
  //sh "curl -ls ${params.servername}:8888/biomni | head -n 1 | cut -c 10-12" > $a
  //sh "echo $a"

  
 }

}
stage("Docker")
 {
  steps
  {
   //sh "curl -fsSL get.docker.com -o get-docker.sh"
   //sh "sh get-docker.sh"
     //withCredentials([

      //[$class: 'UsernamePasswordMultiBinding', credentialsId: 'DockerHubCred', usernameVariable: 'GIT_USER', passwordVariable: 'GIT_PASS'],

 // ])
   sh	"echo  ${GIT_USER}"
sh "echo ${GIT_PASS}"
   
   sh "docker info"
   sh "docker build -t tomcat:tomcat3 ."
   sh "docker images"
   sh "docker login --username shanmukha511 --password  raviteja511"
   sh "docker tag tomcat:tomcat3 shanmukha511/tomcat:tomcat3"
   sh "docker push shanmukha511/tomcat:tomcat3"
   //sh "ssh -tt -v -o StrictHostKeyChecking=no root@${params.servername} 'sudo -i'"
   sh "ssh -tt -v -o StrictHostKeyChecking=no root@${params.servername} 'apt-get update'"
   sh "ssh -tt -v -o StrictHostKeyChecking=no root@${params.servername} 'curl -fsSL get.docker.com -o get-docker.sh|sh get-docker.sh'"
   sh "ssh -tt -v -o StrictHostKeyChecking=no root@${params.servername} 'docker pull shanmukha511/tomcat:tomcat3'"
   sh "ssh -tt -v -o StrictHostKeyChecking=no root@${params.servername} 'docker images'"
   sh "ssh -tt -v -o StrictHostKeyChecking=no root@${params.servername} 'docker run -it -d --name tomcat -p 8080:8888 shanmukha511/tomcat:tomcat3 /bin/bash'"
   sh "ssh -tt -v -o StrictHostKeyChecking=no  root@${params.servername} 'docker ps'"

  }
 }


}

 
}
