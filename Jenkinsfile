pipeline {
    agent any

    environment {
        registry = "hamzadahbani/tp4"
        registryCredential = 'c5ea2ed2-36f6-4547-952f-5f1efde1b50d'
        dockerImage = ''
    }

    stages {
        stage('Cloning Git') {
            steps {
                git 'https://github.com/hamzadahbani/tp4devops'
            }
        }

        stage('Building Image') {
            steps {
                script {
                    dockerImage = docker.build("${registry}:${BUILD_NUMBER}")
                }
            }
        }

        stage('Publish Image') {
            steps {
                script {
                    docker.withRegistry('', registryCredential) {
                        dockerImage.push()
                    }
                }
            }
        }

        stage('Deploy image') {
            steps{
                bat "docker run -d $registry:$BUILD_NUMBER"
            }
        }
    }
}
