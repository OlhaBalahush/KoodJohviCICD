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
        stage('npm install') {
            steps {
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
                    def branchName = sh(script: 'git rev-parse --abbrev-ref HEAD', returnStdout: true).trim()
                    def nameSubDirectory = "olha_${branchName}"

                    def folderName = [
                        'main': 'main',
                        'develop': 'develop'
                    ][branchName]

                    if (folderName) {
                        sh "mkdir -p /kj_deployments/${nameSubDirectory}_${folderName}"
                        sh "cp -r dist/kood-johvi-cicd/browser/* /kj_deployments/${nameSubDirectory}_${folderName}"
                    } else {
                        echo "Branch not recognized for deployment."
                    }
                }
            }
        }
    }
}
