pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                sh 'sleep 3'
                sh 'echo "Hello from Build stage!"'
            }
        }

        stage('Test - edited') {
            steps {
                echo 'Testing...'
                sh 'sleep 3'
                sh 'echo "Running some dummy tests..."'
            }
        }



     stage('Nwe stage 1 ') {
                steps {
                    echo 'Deploying...'
                    sh 'sleep 1'
                    sh 'echo "Pretending to deploy..."'
                    // Intentionally fail the build
                    // sh 'exit 1'
                }
            }

     stage('New stage 2') {
                steps {
                    echo 'Deploying...'
                    sh 'sleep 1'
                    sh 'echo "Pretending to deploy..."'
                    // Intentionally fail the build
                    // sh 'exit 1'
                }
            }
        
    }
}
