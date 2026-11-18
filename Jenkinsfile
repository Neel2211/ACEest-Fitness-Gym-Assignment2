pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Neel2211/ACEest-Fitness-Gym-Assignment2.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'python3 -m ensurepip --default-pip || true'
                sh 'python3 -m pip install --user -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'python3 -m pytest'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                script {
                    def scannerHome = tool 'SonarScanner'

                    withSonarQubeEnv('ACEest-SonarQube') {
                        sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=aceest-fitness-gym-assignment2"
                    }
                }
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t aceest-fitness-gym:v3.2.4 .'
            }
        }

        stage('Docker Hub Push') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub-creds',
                        usernameVariable: 'DOCKER_USER',
                        passwordVariable: 'DOCKER_PASS'
                    )
                ]) {
                    sh '''
                    echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                    docker tag aceest-fitness-gym:v3.2.4 neel72211/aceest-fitness-gym:v3.2.4
                    docker push neel72211/aceest-fitness-gym:v3.2.4
                    '''
                }
            }
        }
    }
}