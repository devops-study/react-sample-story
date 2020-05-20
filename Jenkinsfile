pipeline {
    agent {
        dockerfile true
    }
    environment {
        HOME = '.'
    }

    stages {
        stage('prepare') {
            steps {
                sh 'ls -la'
                sh 'npm ci'
            }
        }
        stage('test') {
            steps {
                sh 'CI=true npm test'
            }
        }
        stage('build') {
            steps {
                sh 'npm run build'
            }
        }
        stage('deploy') {
            steps {
                sh '''
                git config remote.origin.url git@github.com:devops-study/react-sample.git
                ls -la
                pwd
                npm run deploy
                '''
            }
        }
    }
    post {
        failure {
            slackSend color: 'danger', message: "Jenkins job fail.\n${env.BUILD_URL}"
        }
    }
}
