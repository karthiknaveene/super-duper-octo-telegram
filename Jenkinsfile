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
                        sleep 7
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
                        catchError(buildResult: 'UNSTABLE', stageResult: 'UNSTABLE') {
                            echo 'Packaging...'
                            sleep 2
                            echo 'Forcing UNSTABLE status'
                            sh 'exit 1'
                        }
                    }
                }
            }
        }

        stage('Package') {
            steps {
                echo 'Registering the metadata'
                echo 'Another echo to make the pipeline a bit more complex'
                sleep 40
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
                script {
                    echo "Starting Package-2 tests..."
                    sleep 5

                    echo "Aborting this stage intentionally..."
                    // This throws an InterruptedException → Jenkins marks stage ABORTED
                    error("ABORTED_BY_SCRIPT")
                }
            }
        }

        stage('Build-2') {
            stages {
                stage('Compile') {
                    steps {
                        echo 'Compiling...'
                        sleep 4
                    }
                }
                stage('Package') {
                    steps {
                        catchError(buildResult: 'UNSTABLE', stageResult: 'UNSTABLE') {
                            echo 'Packaging...'
                            sleep 2
                            echo 'Forcing UNSTABLE status'
                            sh 'exit 1'
                        }
                    }
                }
            }
        }

        stage('Deploy') {
            when {
                expression {
                    // skip deploy if aborted
                    currentBuild.result != 'ABORTED'
                }
            }
            steps {
                echo 'Deploying...'
                sleep 5
            }
        }
    }
}
