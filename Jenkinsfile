/* import shared library */
@Library('jenkins-shared-library')_

pipeline {
    agent none
    stages {
        stage('Check Dockerfile syntax') {
            agent { docker { image 'hadolint/hadolint' } }
            steps {
             script { dockerfileCheck }
            }
        }

        stage('Check Golang syntax') {
            agent { docker { image 'appleboy/golang-testing' } }
            steps {
             script { golangCheck }
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
        
         stage('Check Css syntax') {
            agent { docker { image 'hspaans/csslint' } }
            steps {
             script { cssCheck }
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
