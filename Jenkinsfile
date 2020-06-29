/* import shared library */
@Library('jenkins-shared-library')_

pipeline {
    agent none
    stages {
        /*stage('Check python syntax') {
            agent { docker { image 'eeacms/pylint' } }
            steps {
                sh 'pylint  \${WORKSPACE}/simple_api/student_age.py'
            }
        }*/
        stage('Check docker-compose syntax') {
            agent { docker { image 'docker/compose' } }
            steps {
                sh 'docker-compose -f \${WORKSPACE}/docker-compose.yml config'
            }
        }
        /*stage('Check Dockerfile syntax') {
            agent { docker { image 'hadolint/hadolint' } }
            steps {
                sh 'hadolint \${WORKSPACE}/simple_api/Dockerfile'
            }
        }*/
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
