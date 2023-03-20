pipeline {
    environment{
        imageName=""
    }
    agent any
    stages {
        stage('Git pull') {
            steps {
                git branch:'main', url : 'https://github.com/anshulsankhyan/Calculator.git'
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
        stage('Deploy') {
            steps {
                ansiblePlaybook becomeUser: null, colorized: true, disableHostKeyChecking: true, installation: 'Ansible', inventory: 'deploy-docker/inventory',
                 playbook: 'deploy-docker/deploy.yml', sudoUser: null, extras: '-e "image_name=anshulsankhyan98/spe_mini_project"'
            }
        }
    }
}
