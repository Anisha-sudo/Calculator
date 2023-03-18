pipeline {
    environment{
        imageName=""
    }
    agent any
    stages {
        stage('Git pull') {
            steps {
                git 'https://github.com/Anisha-sudo/Calculator.git'
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
                    imageName=docker.build "anisha0987/spe_mini_project"
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
//         stage('Deploy') {
//             steps {
//                 ansiblePlaybook becomeUser: null, colorized: true, disableHostKeyChecking: true, installation: 'Ansible', inventory: 'deploy-docker/inventory',
//                  playbook: 'deploy-docker/deploy.yml', sudoUser: null, extras: '-e "image_name=anshulsankhyan98/spe_mini_project"'
//             }
//         }
    }
}