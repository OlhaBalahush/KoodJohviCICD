pipeline {
    agent any
    
    tools {
        nodejs 'nodejs21'
    }

    stages {
        stage('Hello') {
            steps {
                git branch: 'main', url: 'https://github.com/OlhaBalahush/KoodJohviCICD.git'
            }
        }
        stage('npm install'){
            steps{
                script {
                    sh 'npm install'
                }
            }
        }
        stage('build application') {
            steps {
                script {
                    sh 'npm run build'
                }
            }
        }
        stage('deploy application') {
            steps {
                script {
                    sh "mkdir -p /kj_deployments/subDir"
                    sh "cp -r dist/kood-johvi-cicd/browser/* /kj_deployments/subDir"
                }
            }
        }
        stage('discord notification') {
            steps {
                discordSend description: '', footer: '', image: '', link: 'https://discordapp.com/api/webhooks/1180074515070459914/zl9CXKo6somXD5WPFVMi4wizdGQ-KMDuypK1GKuyA-LvkWHEfoKcfcYhbRwIY1_63Drh', result: 'FAILURE', scmWebUrl: '', thumbnail: '', title: 'Sending message', webhookURL: 'https://sebkoodjohvi.duckdns.org/generic-webhook-trigger/invoke?token=olyaToken'
            }
        }
    }
}
