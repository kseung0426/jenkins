pipeline {
    agent any 
    options {
        timestamps()  // 타임스탬프 옵션 활성화
    }
    stages {
        stage('CheckOut') { 
            steps {
                echo "CheckOut" 
            }
        }
        stage('Build') { 
            steps {
                echo "Build" 
            }
        }
        stage('Deploy') { 
            steps {
                echo "Deploy"
            }
        }
    }

    post {
        always {
            script {
                def jobResult = currentBuild.result ?: 'SUCCESS'
                if (params.Email_Notification_Method == 'All Status') {
                    build job: 'ksg-playground/alert-notificate-trigger',
                          parameters: [
                              string(name: 'SOURCE_JOB_URL', value: "${env.JOB_URL}"),
                              string(name: 'SOURCE_BUILD_NUMBER', value: "${env.BUILD_NUMBER}"),
                              string(name: 'SOURCE_BUILD_URL', value: "${env.BUILD_URL}"),
                              string(name: 'SOURCE_NODE_NAME', value: "${env.NODE_NAME}"),
                              string(name: 'SOURCE_JOB_BASE_NAME', value: "${env.JOB_BASE_NAME}"),
                              string(name: 'SOURCE_JOB_RESULT', value: jobResult),
                              string(name: 'SOURCE_EMAIL_RECIPIENTS', value: "${params.Email_Recipients}")
                          ]
                } else if (params.Email_Notification_Method == 'Exclude Success' && jobResult != 'SUCCESS') {
                    build job: 'ksg-playground/alert-notificate-trigger',
                          parameters: [
                              string(name: 'SOURCE_JOB_URL', value: "${env.JOB_URL}"),
                              string(name: 'SOURCE_BUILD_NUMBER', value: "${env.BUILD_NUMBER}"),
                              string(name: 'SOURCE_BUILD_URL', value: "${env.BUILD_URL}"),
                              string(name: 'SOURCE_NODE_NAME', value: "${env.NODE_NAME}"),
                              string(name: 'SOURCE_JOB_BASE_NAME', value: "${env.JOB_BASE_NAME}"),
                              string(name: 'SOURCE_JOB_RESULT', value: jobResult),
                              string(name: 'SOURCE_EMAIL_RECIPIENTS', value: "${params.Email_Recipients}")
                          ]
                } else if (params.Email_Notification_Method == 'None') {
                    echo """
###############################################################################################
${JOB_BASE_NAME} Finished Without sending Email
###############################################################################################
"""
                }
            }
        }
    }
}
