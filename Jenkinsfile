      
node {
   def mvnHome
   stage('Preparation') { // for display purposes
      // Get some code from a GitHub repository
      git url: 'https://github.com/harijayan1797/ashok.git'
      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured
      // **       in the global configuration.           
      mvnHome = tool 'M3'
   }
   stage('Build') {
      // Run the maven build
      withEnv(["MVN_HOME=$mvnHome"]) {
         if (isUnix()) {
            sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore clean package'
         } else {
            bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore clean package/)
         }
      }
   }
   stage('Results') {
      junit '**/target/surefire-reports/TEST-*.xml'
     //junit '**/something/surefire-reports/TEST-*.xml'
      archiveArtifacts 'target/*.jar'
  
      //gsutil cp 'target/*.jar' 'gs://jenkins--bucket'
     // scp 'target/*.jar' 'https://console.cloud.google.com/storage/browser/jenkins--bucket'
   }
   stage('Google Cloud Storage Push') {
      //gsutil cp 'target/*.jar' 'gs://jenkins--bucket'
    googleStorageUpload bucket: 'gs://project-bucket1', credentialsId: 'instance-32537', pattern: 'target/*.jar'
   }
  

}






   /* node {
    stage('Clone sources') {
        git url: 'https://github.com/harijayan1797/ashok.git'
    }
  stage('Mvn Package'){
      sh label: '', script: 'mvn  clean  package'
  }
  stage('Build Docker Imager'){
   sh 'sudo docker build -t gcr.io/jenkins-250111/tomcat . '
   sh 'gcloud auth configure-docker'
  }
  stage('Push image') {
      withDockerRegistry(credentialsId: 'gcr:jenkins_gcr', url: 'https://gcr.io'){
        sh label: '', script: 'sudo docker push gcr.io/jenkins-250111/tomcat'
    }
  }
}*/
