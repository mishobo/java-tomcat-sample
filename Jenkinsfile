Pipeline {
    agent any
    stages {
        stage ('Build Application') {
            steps {
                sh 'mvn clean packages'
            }
            post {
                success {
                    echo 'Now archiving the artifacts.....'
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }
    }
}