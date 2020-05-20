pipeline {
    agent {
        docker {
            image 'node:12.16.3-slim'
        }
    }

    stages {
        stage('prepare') {
            steps {
                cleanWs()
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
