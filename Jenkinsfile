node(''){
 
 properties([
    buildDiscarder(logRotator(numToKeepStr: '3')),
    pipelineTriggers([
        pollSCM('* * * * *')
    ])
])

 def mavenHome = tool name: 'maven3.6.1', type: 'maven'
 
 stage('CheckoutCode') {
 git branch: 'master',  credentialsId: 'fd6b0c23-4d78-4be1-8f6f-5d491069c66a', url: 'https://github.com/saharamayyadi/maven-web-application.git'
 }  
  
  stage('Build') {
 
    sh "${mavenHome}/bin/mvn clean package"
  }

  stage('ExecuteSonarQubeRreport') {
 
 sh "${mavenHome}/bin/mvn sonar:sonar"
 }     
  
  stage('UploadArtifactIntoNexus') {
 
 sh "${mavenHome}/bin/mvn deploy"
 } 
 
 stage('DeployAppIntoTomcat'){
  sh "cp $WORKSPACE/target/*.war /opt/apache-tomcat-9.0.19/webapps/"
  } 
}
