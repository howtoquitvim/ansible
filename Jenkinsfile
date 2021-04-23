pipeline {
    environment {
        imagename = "fateevilia/epamexam"
        app_url = "http://192.168.0.17:88"
    }
    agent JenkAgent
    stages {
        stage('Deploy') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'imagepush', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    ansiblePlaybook( 
                            playbook: 'run.yml',
                            inventory: 'hosts', 
                            credentialsId: 'deploy',
                            extras: '--ssh-extra-args="-o StrictHostKeyChecking=no" -e hub_login=${USERNAME} -e hub_password=${PASSWORD} -e imagename=${imagename}')
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    httpRequest app_url
                }
            }
        }
    }
}
