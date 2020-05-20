pipeline {
    agent any

    stages {
        stage('git clone') {
            steps {
                git 'git@github.com:devops-study/react-sample.git'
            }
        }
        stage('prepare') {
            steps {
                nodejs('NodeJS_12.16.3') {
                    sh 'npm ci'
                }
            }
        }
        stage('test') {
            steps {
                nodejs('NodeJS_12.16.3') {
                    sh 'CI=true npm test'
                }
            }
        }
        stage('build') {
            steps {
                nodejs('NodeJS_12.16.3') {
                    sh 'npm run build'
                }
            }
        }
        stage('deploy') {
            steps {
                nodejs('NodeJS_12.16.3') {
                    sh 'npm run deploy'
                }
            }
        }
    }
    post {
        failure {
            slackSend color: 'danger', message: "Jenkins job fail.\n${env.BUILD_URL}"
        }
    }
}
