pipeline {
    agent {
        node {
            label 'maven'
        }
    }
environment{
    PATH = "/opt/apache-maven-3.9.9/bin:$PATH"
}
    stages {
        stage("build"){
            steps {
                sh 'mvn clean deploy -Dmaven.test.skip=true'
                 echo "build completed"
            }
        }
        stage("test"){
            steps {
                sh 'mvn surefire-report:report'
                 echo "unit test copleted"
            }
        }
    stage('SonarQube analysis') {
    environment {
        scannerHome = tool 'brajesh540-sonar-scanner';
    }
    steps{
    withSonarQubeEnv('brajesh540-sonarqube-server') { // If you have configured more than one global server connection, you can specify its name
      sh "${scannerHome}/bin/sonar-scanner"
    }
  }
    }
}
}