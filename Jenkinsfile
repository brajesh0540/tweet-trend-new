pipeline {
    agent {
        node {
            label 'maven'
        }
    }

    stages {
        stage('clone code') {
            steps {
                git branch: 'main', url: 'https://github.com/brajesh0540/tweet-trend-new.git'
            }
        }
    }
}