pipeline {
    agent any
    stages {
        stage('Pull Code From GitHub') {
            steps {
                git 'https://github.com/ajayaj3008/devopsproject04.git' 
            }
        }
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv("sonar") {
                    sh '/opt/sonar-scanner/bin/sonar-scanner'
                }
            }
        }
        stage('Build the Docker image') {
            steps {
                sh 'docker build -t new image .'
                }
            }
    }
}
