pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials("dockerhub")
        DOCKER_REGISTRY = "denture8278"
        DOCKER_NAME = "devops-final-order"
        // DOCKER_TAG = "${env.BUILD_NUMBER}"  // todo
        DOCKER_TAG = "v1.1"
    }

    stages {
        stage('Build') {
            steps {
                script {
                    utils.buildAPI()
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    utils.testJavascript()
                }
            }
        }
        stage('Security Scan') {
            steps {
                script {
                    utils.runStaticScan()
                }
            }
        }
        stage('Container Build') {
            steps {
                script {
                    utils.buildDocker(
                        DOCKER_REGISTRY, 
                        DOCKER_NAME, 
                        DOCKER_TAG
                    )
                }
            }
        }
        stage('Container Push') {
            steps {
                script {
                    utils.pushDocker(
                        DOCKER_REGISTRY, 
                        DOCKER_NAME, 
                        DOCKER_TAG,
                        DOCKERHUB_CREDENTIALS_USR,
                        DOCKERHUB_CREDENTIALS_PSW,
                    )
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    utils.conditionalDeployment(
                        env.branchName
                    )
                }
            }
        }
    }

    post {
        always {
            sh 'docker logout'
        }
    }
}
