pipeline {
    agent {
  label 'server1-martinsolihin'
}
    
//    tools {nodejs "nodejs 18.16.0"}

    stages {
        stage('Checkout SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/martinsolihin/simple-apps.git'
            }
        }
        stage('Build') {
            steps {
                sh '''cd apps
                npm install'''
            }
        }
        stage('Testing') {
            steps {
                sh '''cd apps
                npm test
                npm run test:coverage'''
            }
        }
        stage('Code Review') {
            steps {
                sh '''cd apps
                sonar-scanner \
                -Dsonar.projectKey=Simple-Apps \
                -Dsonar.sources=. \
                -Dsonar.host.url=http://172.23.14.105:9000 \
                -Dsonar.login=sqp_4960c04a5f0b8170b677db0fcd4b59362584c9e8'''
            }
        }
        stage('Deploy compose') {
            steps {
                sh '''
                docker compose build
                docker compose up -d
                '''
            }
        }
    }
}