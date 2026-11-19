pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Environment Validation') {
            steps {
                sh 'python3 --version'
                sh 'git --version'
                sh 'docker --version'
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

        stage('Read Version') {
            steps {
                script {
                    env.APP_VERSION = sh(
                        script: 'cat VERSION',
                        returnStdout: true
                    ).trim()

                    echo "Building version: ${env.APP_VERSION}"
                }
            }
        }

        stage('Docker Build') {
            steps {
                sh """
                docker build -t aceest-fitness-gym:${env.APP_VERSION} .
                """
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
                    sh """
                    echo "${DOCKER_PASS}" | docker login -u "${DOCKER_USER}" --password-stdin

                    docker tag aceest-fitness-gym:${env.APP_VERSION} \
                    neel72211/aceest-fitness-gym:${env.APP_VERSION}

                    docker push neel72211/aceest-fitness-gym:${env.APP_VERSION}
                    """
                }
            }
        }
    }

    post {
        success {
            echo 'Build completed successfully'
        }

        failure {
            echo 'Build failed'
        }
    }
}