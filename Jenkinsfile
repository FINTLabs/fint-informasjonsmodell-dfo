pipeline {
    agent none
    stages {
        stage('Trigger model generation') {
            agent { label 'master' }
            when {
                expression { BRANCH_NAME ==~ /v\d+\.\d+\.\d+(-\w+-\d+)?/ }
            }
            steps {
                script {
                    VERSION = BRANCH_NAME[1..-1]
                }
                sh "echo Version is ${VERSION}"
                build job: '/fint-devops-model-release', parameters: [
                    string(name: 'MODEL_VERSION', value: "${VERSION}"),
                    string(name:'VERSION', value: "${VERSION}")]
            }
        }
    }
}