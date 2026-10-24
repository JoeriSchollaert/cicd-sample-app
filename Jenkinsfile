pipeline {
    agent any
    stages {
        stage('Preparation') {
            steps {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    sh 'docker stop samplerunning'
                    sh 'docker rm samplerunning'
                }
            }
        }
        stage('Build') {
            steps {
                build 'BuildSampleApp'
            }
        }
        stage('Results') {
            steps {
                build 'TestSampleApp'
            }
        }
        stage('Deploy op Host') {
            steps {
                sshPublisher(
                    publishers: [
                        sshPublisherDesc(
                            configName: 'infra010',
                            transfers: [
                                sshTransfer(execCommand: 'cd /home/vagrant/dotnet-demo-app && docker compose up -d --build')
                            ]
                        )
                    ]
                )
            }
        }
    }
}