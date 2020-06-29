/* import shared library */
@Library('jenkins-shared-library')_

pipeline {
    agent none
    stages {
        stage('Check Dockerfile syntax') {
            agent { docker { image 'hadolint/hadolint' } }
            steps {
                sh '/bin/hadolint  \${WORKSPACE}/fake-backend/Dockerfile'
            }
        }

        stage('Check Golang syntax') {
            agent { docker { image 'cytopia/golint' } }
            steps {
                sh 'golint  \${WORKSPACE}/fake-backend/'
                sh 'golint  \${WORKSPACE}/fake-backend/vendor/github.com/go-sql-driver/mysql/'
            }
        }
    }
    post {
    always {
       script {
         /* Use slackNotifier.groovy from shared library and provide current build result as parameter */
         clean
         slackNotifier currentBuild.result
     }
    }
    }
}
