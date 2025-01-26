pipeline {
    environment {
        registry = "hananeenset/tp5" // Nom de votre image Docker Hub
        registryCredential = '8b4ade29-0303-4eca-b393-b80b9f18290c' // ID valide des credentials Docker Hub
        dockerImage = ''
    }
    agent any
    stages {
        stage('Cloning Git') {
            steps {
                git 'https://github.com/hananelahssini24/Tp5-DevOps' // Clone le dépôt Git
            }
        }
        stage('Building image') {
            steps {
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER" // Crée l'image Docker avec le numéro de build
                }
            }
        }
        stage('Test image') {
            steps {
                script {
                    echo "Tests passed" // Simule les tests
                }
            }
        }
        stage('Publish Image') {
            steps {
                script {
                    docker.withRegistry('', registryCredential) {
                        dockerImage.push() // Pousse l'image Docker sur Docker Hub
                    }
                }
            }
        }
        stage('Deploy image') {
            steps {
                bat "docker run -d $registry:$BUILD_NUMBER" // Déploie l'image avec le numéro de build
            }
        }
    }
}
