  
    node {
    stage('Clone sources') {
        git url: 'https://github.com/harijayan1797/ashok.git'
    }
  stage('Mvn Package'){
      sh label: '', script: 'mvn  clean  package'
  }
  stage('Build Docker Imager'){
   sh 'sudo docker build -t gcr.io/jenkins-250111/tomcat . '
  }
  stage('Push image') {
      withDockerRegistry(credentialsId: 'gcr:jenkins_gcr', url: 'https://gcr.io'){
        sh label: '', script: 'sudo docker push gcr.io/jenkins-250111/tomcat'
    }
  }
}
