node {
    stage('Preparation') {
        catchError(buildResult: 'SUCCESS') {
            sh 'docker stop samplerunning'
            sh 'docker rm samplerunning'
        }
    }
    stage('Build') {
        build 'BuildSampleApp'
    }
    stage('Results') {
        build 'TestSampleApp'
    }
    stage('Deploy op Host') {
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
