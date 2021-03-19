node{
    def mavenHome = tool name: "maven3.6.3"
  stage('CheckoutCode') 
  {
      git branch: 'development', credentialsId: '72009d1c-3b7b-4952-ab20-4231fddc844b', url: 'https://github.com/MithunTechnologiesCode/maven-web-application.git'
  } 
  stage('Build')
  {
      sh "${mavenHome}/bin/mvn clean package"
  }
  stage('ExxecuteSonarQubeReport')
  {
      sh "${mavenHome}/bin/mvn sonar:sonar"
  }
  stage('UploadArtifactIntoNexus')
  {
      sh "${mavenHome}/bin/mvn deploy"
  }
  stage('DeployAppintoTomcatServer')
  {
     sshagent(['19a8b4c2-41a1-4209-ae76-0f5194d6d888']) {
         sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@54.84.125.251:/opt/tomcat9/webapps/"
     }
  }
}
