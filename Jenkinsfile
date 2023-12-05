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
            when {
                expression { 
                    return (env.BRANCH_NAME == 'olha_main' || env.BRANCH_NAME == 'olha_develop')
                }
            }
            steps {
                script {
                    def branchName = env.BRANCH_NAME
                    def nameSubDirectory = "olha_${branchName}"

                    sh "mkdir -p /kj_deployments/${nameSubDirectory}"
                    sh "cp -r dist/kood-johvi-cicd/browser/* /kj_deployments/${nameSubDirectory}"
                }
            }
        }
    }
}
