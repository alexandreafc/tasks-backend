pipeline {
    agent any
    stages {
        stage ('Build backend') {
            steps {
                sh 'mvn clean package -DskipTests=true'
            }
        }
        stage ('Unit Tests') {
            steps {
                sh 'mvn test'
            }
        }
        stage ('Sonar Analysis') {
            environment {
                scannerHome = tool 'SONAR_SCANNER'
            }
            steps {
                withSonarQubeEnv('SONAR_LOCAL') {
                    sh "${scannerHome}/bin/sonar-scanner -e -Dsonar.projectKey=DeployBack -Dsonar.host.url=http://sonar:9000 -Dsonar.login=c0159fd2e22acce2a6982dc731ff5b04d519accb -Dsonar.java.binaries=target"
                }
            }
        }
    }
}