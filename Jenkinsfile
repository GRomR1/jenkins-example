
pipeline {
    agent any
    stages {
        stage('Stage 1') {
            steps {
                echo 'Hello world!'
                echo "Build number is ${currentBuild.number}"
                echo "env.BUILD_ID is ${env.BUILD_ID}"
            }
        }
        
        stage('Example Username/Password') {
            environment {
                SERVICE_CREDS = credentials('my-predefined-username-password')
            }
            steps {
                sh 'echo "Service user is $SERVICE_CREDS_USR"'
                sh 'echo "Service password is $SERVICE_CREDS_PSW"'
                sh 'curl -v -u $SERVICE_CREDS https://httpbin.org/basic-auth/admin/admin'
            }
        }

        stage ('Invoke_pipeline') {
            steps {
                echo 'See job results on project "jenkins-example-child"'
                build job: 'jenkins-example-child', parameters: [
                  string(name: 'param1', value: "${env.BUILD_ID}")
                ]
            }
        }

    }
}
