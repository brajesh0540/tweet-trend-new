def registry = 'https://brajesh540.jfrog.io/'
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
    //stage('SonarQube analysis') {
    //environment {
        //scannerHome = tool 'brajesh540-sonar-scanner';
    //}
    //steps{
    //withSonarQubeEnv('brajesh540-sonarqube-server') { // If you have configured more than one global server connection, you can specify its name
      //sh "${scannerHome}/bin/sonar-scanner"
    //}
  //}
    //}
    stage("Jar Publish") {
        steps {
            script {
                    echo '<--------------- Jar Publish Started --------------->'
                     def server = Artifactory.newServer url:registry+"/artifactory" ,  credentialsId:"artifact_cred"
                     def properties = "buildid=${env.BUILD_ID},commitid=${GIT_COMMIT}";
                     def uploadSpec = """{
                          "files": [
                            {
                              "pattern": "jarstaging/(*)",
                              "target": "brajesh540-libs-release-local/{1}",
                              "flat": "false",
                              "props" : "${properties}",
                              "exclusions": [ "*.sha1", "*.md5"]
                            }

                         ]
                     }"""
                     def buildInfo = server.upload(uploadSpec)
                     buildInfo.env.collect()
                     server.publishBuildInfo(buildInfo)
                     echo '<--------------- Jar Publish Ended --------------->'  
            
            }
        }   
    }   
}
}