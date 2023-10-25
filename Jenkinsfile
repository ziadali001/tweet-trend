pipeline {
    agent {
        node{
            label 'maven'
        }
    }

environment {
    PATH = "/opt/apache-maven-3.9.5/bin:$PATH"
}

    stages {
        stage('Build') {
            steps {
                sh 'mvn clean deploy -Dmaven.test.skip=true'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn surefire-report:report'
            }
        }

        stage('SonarQube analysis') {
        environment {
            scannerHome = tool 'devops-sonar-scanner'
        }
            steps{
            withSonarQubeEnv('devops-sonarqube-server') {
                sh "${scannerHome}/bin/sonar-scanner"
            }
            }
        }
    }    
}
