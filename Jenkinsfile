
pipeline {
    agent any
    options {
        copyArtifactPermission('jenkins-example-child');
    }
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
                sh 'curl -sS -u $SERVICE_CREDS https://httpbin.org/basic-auth/admin/admin'
            }
        }

        stage ('Invoke_pipeline') {
            steps {
                echo 'See job results on project "jenkins-example-child"'
                sh """
                  echo "Downstream project is ${env.JOB_NAME}" > downstream_artifact.txt
                """
                // https://www.jenkins.io/doc/pipeline/steps/pipeline-build-step/
                build job: 'jenkins-example-child', parameters: [
                  string(name: 'param1', value: "${env.BUILD_ID}")
                ]

                echo "Child project result is ${currentBuild.currentResult}"
                echo "Child project result is ${currentBuild.result}"

                sh """
                  echo "Build result is ${currentBuild.currentResult}" > result.txt
                """
            }
        }

    }

    post {
        always {
            archiveArtifacts artifacts: '*.txt', fingerprint: true
        }
    }
}
