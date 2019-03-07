pipeline {
    agent {
        docker {
            image 'node:6-alpine' 
            args '-p 3000:3000' 
        }
    }
    environment {
        CI = 'true'
    }
    stages {
        stage('Build') { 
            steps {
                sh 'npm install' 
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Package') {
            steps {
                sh './jenkins/scripts/package.sh'
            }
        }
        stage('Cleanup') {
            steps {
                deleteDir()
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'package.tar.gz', fingerprint: true
        }
    }
}
