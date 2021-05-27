node{
    
    def mavenHome = tool name: "maven3.6.3"

stage('1.Github Clone code')

{
git branch: 'dev', credentialsId: 'c980f791-7892-4df5-bcf7-51e5ff33abc1', url: 'https://github.com/ebay-organ/maven-web-app.git'

}

stage('2.Maven Build package')

{
 sh "${mavenHome}/bin/mvn clean package"
  //bat "${mavenHome}/bin/mvn clean package" for window system
}

stage('3.Sonarqube codeQuality Report')
{
sh "${mavenHome}/bin/mvn clean package sonar:sonar"
//bat "${mavenHome}/bin/mvn clean package sonar:sonar" for windows system
}
stage('4.Nexus UploadArtifact')
{
sh "${mavenHome}/bin/mvn clean deploy"
//bat "${mavenHome}/bin/mvn clean deploy" for windows system
}

stage('5.Tomcat Deploy')
{

deploy adapters: [tomcat9(credentialsId: 'Tomcat_credential', path: '', url: 'http://3.236.146.26:7777')], contextPath: null, war: '**/*.war'

}

stage('6 Email Notification')
{
emailext body: 'Build Performed take note on the executor', recipientProviders: [developers()], subject: 'Build Status', to: 'evandango@outlook.com'
}
}
