
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
        
        stage ('Invoke_pipeline') {
            steps {
                build job: 'jenkins-example-child', parameters: [
                string(name: 'param1', value: "value1")
                ]
            }
        }

    }
}
