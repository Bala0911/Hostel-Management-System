pipeline{
    agent any
    environment{
        staging_server="172.31.33.248"
    }
    // 
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



pipeline {
    agent any
    environment{
        staging_server="172.31.4.102"
        // deploy_server="172.31.45.114"
    }
    stages {
        stage ('Checkout') {
            steps {
                // checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[refspec: 'refs/tags/v1', url: 'https://github.com/bala-09/Hostel-Management-System.git']])
                git branch: 'main', credentialsId: 'aws-codecommit', url: 'https://git-codecommit.ap-south-1.amazonaws.com/v1/repos/Repo'
            }
        }
        stage ('Depoy to server') {
            input {
                message "Do you proceed?"
            }
            steps {
                sh 'rsync -avzh * --delete --exclude=.git --exclude=.gitignore --exclude=.gitattributes --exclude=README.md . ubuntu@${staging_server}:/var/www/html/'
            }
        }
        
    }
}
