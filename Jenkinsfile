pipeline {
    agent any

    stages {

        stage('Build') {
            stages {
                stage('Compile') {
                    steps {
                        script {
                            echo "Compiling (Build stage)..."
                            sleep 2
                            echo "Marking Build/Compile as SUCCESS"
                            currentBuild.result = "SUCCESS"
                        }
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

        stage('Compile') {
            steps {
                script {
                    echo 'Registering metadata...'
                    sleep 3
                    echo 'Another echo for complexity...'

                    // Set this compile step to UNSTABLE
                    echo "Marking standalone Compile as UNSTABLE"
                    currentBuild.result = "UNSTABLE"

                    registerBuildArtifactMetadata(
                        name: "Internal-demo-runs-BT",
                        version: "1.0.1",
                        type: "docker",
                        url: "http://localhost:4001",
                        digest: "6f637064707039346163663761",
                        label: "artifact"
                    )
                }
            }
        }

        stage('Package') {
            steps {
                echo 'Running Unit Tests...'
                sleep 2
                echo 'Running Integration Tests...'
                sleep 5
            }
        }

        stage('Build-2') {
            stages {
                stage('Compile') {
                    steps {
                        script {
                            echo 'Compiling (Build-2 stage)...'
                            sleep 5

                            echo "Marking Build-2/Compile as FAILURE"
                            currentBuild.result = "FAILURE"
                        }
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

        stage('Deploy') {
            when {
                expression { currentBuild.resultIsBetterOrEqualTo("UNSTABLE") }
            }
            steps {
                echo 'Deploying...'
                sleep 5
            }
        }
    }
}
