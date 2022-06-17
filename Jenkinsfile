pipeline {
    agent any
 stages {	
stage('Source Code Checkout') {
	steps{
    git '$git_url'
}
}
  stage('Build - Maven') {
    steps {
	sh 'mvn install -DskipTests'
}
}
  stage('Nexus Deploy') {
	steps {
   nexusArtifactUploader artifacts: [[artifactId: 'UAT', classifier: '', file: 'gameoflife-web/target/gameoflife.war', type: 'war']], credentialsId: '675c31e8-8de1-4f2d-b44b-f38e07113364', groupId: 'UAT', nexusUrl: '35.88.47.128:8081/nexus/#view-repositories', nexusVersion: 'nexus2', protocol: 'http', repository: 'gol', version: '2.$BUILD_ID'
}
}
}
}
