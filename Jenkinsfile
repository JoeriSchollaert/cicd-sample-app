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
    stage('Deploy DotNet App') {
        dir('dotnet-demo-app/TodoApp') {
            sh 'docker-compose up -d --build'
        }
    }
}
