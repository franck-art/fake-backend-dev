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
            agent { docker { image 'golang:latest' } }
            steps {
                sh 'go get -u golang.org/x/lint/golint'
                sh 'go list -f {{.Target}} golang.org/x/lint/golint'
                sh 'export PATH="$PATH:/go/bin/"'
                sh 'golint  \${WORKSPACE}/fake-backend/'
                sh 'golint  \${WORKSPACE}/fake-backend/vendor/github.com/go-sql-driver/mysql/'
            }
        }
     
       /* stage('Check NodeJs syntax') {
            agent { docker { image 'node:latest' } }
            steps {
                sh 'npm install -g jshint'
                sh 'npm install --save-dev jshint'
                sh 'jshint  \${WORKSPACE}/battleboat/js/battleboat.js'
            }
        } */
        
         stage('Check html syntax') {
            agent { docker { image 'ekostadinov/web-linters' } }
            steps {
                sh 'csslint  \${WORKSPACE}/battleboat/css/styles.css'
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
