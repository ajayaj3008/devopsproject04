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
                sh 'docker build -t newimage .'
                }
            }
        stage('Image Scan') {
            steps {
                sh 'trivy image newimage:latest > report.txt'
                }
            }
        stage('Push to ECR') {
            steps {
                withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'aws-creds']]) {
                    sh '''
                        aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 122610503302.dkr.ecr.ap-south-1.amazonaws.com/myrepo
                        docker tag newimage:latest 122610503302.dkr.ecr.ap-south-1.amazonaws.com/myrepo:latest
                        docker push 122610503302.dkr.ecr.ap-south-1.amazonaws.com/myrepo:latest
                    '''
                    }
                }
            }
    }
}
