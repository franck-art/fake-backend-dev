/* import shared library */
@Library('jenkins-shared-library')_

pipeline {
    agent none
    stages {
        stage('Check Dockerfile syntax') {
            agent { docker { image 'replicated/dockerfilelint' } }
            steps {
                sh 'dockerfilelint  \${WORKSPACE}/fake-backend/Dockerfile'
            }
        }

        stage('Check Golang syntax') {
            agent { docker { image 'cytopia/golint' } }
            steps {
                sh 'golint  \${WORKSPACE}/fake-backend/config.go'
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
