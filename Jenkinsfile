pipeline {
    environment{
        imageName=""
    }
    agent any
    stages {
        stage('Git pull') {
            steps {
                git 'https://github.com/anshulsankhyan/Calculator.git'
            }
        }
        stage('Maven Build') {
            steps {
                script{
                    sh 'mvn clean install'
                }
            }
        }
        stage('Docker Build to Image') {
            steps {
                script{
                    imageName=docker.build "anshulsankhyan98/spe_mini_project"
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script{
                    docker.withRegistry('','docker-jenkins'){
                        imageName.push()
                    }
                }
            }
        }
    }
}
