pipeline {
    agent any
    stages {
        stage ('Build Application') {
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Now archiving the artifacts.....'
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }
        stage ('Deploy in staging environment') {
            steps {
                build job: 'DeployAppStaging'
            }
        }
        stage ('Deploy in production environment') {
            steps {
                timeout(time:5, unit:'DAYS'){
                    input message: 'Approve PRODUCTION Deployment?'
                }
                build job: 'DeployAppProd'
            }
        }
    }
}