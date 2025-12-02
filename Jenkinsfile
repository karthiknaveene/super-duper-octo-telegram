pipeline {
    agent any

    stages {
        stage('Build') {
            stages {
                stage('Compile') {
                    steps {
                        echo 'Compiling...'
                        sleep 10
                    }
                }
                stage('Package') {
                    steps {
                        echo 'Packaging...'
                        sleep 5
                    }
                }
            }
        }

        stage('Build-1') {
            stages {
                stage('Compile') {
                    steps {
                        echo 'Compiling...'
                        sleep 3
                    }
                }
                stage('Package') {
                    steps {
                        echo 'Packaging...'
                        sleep 2
                        exit 1
                    }
                }
            }
        }

        stage('Package') {
            steps {
                echo 'Registering the metadata'
                echo 'Another echo to make the pipeline a bit more complex'
                sleep 4
                registerBuildArtifactMetadata(
                    name: "Internal-demo-runs-BT",
                    version: "1.0.1",
                    type: "docker",
                    url: "http://localhost:4001",
                    digest: "6f637064707039346163663237383761",
                    label: "artifact"
                )
            }
        }

        stage('Package-1') {
            steps {
                echo 'Running Unit Tests...'
                sleep 10
                echo 'Running Integration Tests...'
                sleep 2
            }
        }

         stage('Package-2') {
            steps {
                echo 'Running Unit Tests...'
                sleep 5
                echo 'Running Integration Tests...'
                sleep 5
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying...'
                sleep 5
            }
        }
    }
}
