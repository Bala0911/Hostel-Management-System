pipeline{
    agent any
    environment{
        staging_server="172.31.33.248"
    }
    stages{
        stage('SCM Checkout') {
            steps {
                git credentialsId: 'github-token', branch: 'master', url: 'https://github.com/Bala0911/Hostel-Management-System.git'   
            }
        }
        stage('Deploy to Dev Server'){
        input {
            message "Do you want to proceed for deployment?"
        }
        steps {
            sh 'ssh -o StrictHostKeyChecking=no ubuntu@${staging_server}'
            sh 'rsync -avzh * --delete . --exclude=.git --exclude=README.md ubuntu@${staging_server}:/var/www/html/'
        }
        }
    // stage('Deploy to Dev Server-new'){
    //     input {
    //         message "Do you want to proceed for deployment?"
    //     }
    //     steps {
    //         // git credentialsId: 'github-token', branch: 'dev', url: 'https://github.com/Bala0911/php-web-app.git'
    //         // sh 'ssh -o StrictHostKeyChecking=no ubuntu@${staging_server}'
    //         sh 'rsync -avzh * --delete . --exclude=.git --exclude=README.md ubuntu@${staging_server}:/var/www/html/'
    //         }
    //     }
    }
}
