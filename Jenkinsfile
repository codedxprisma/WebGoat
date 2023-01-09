pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                withCredentials([
                    string(credentialsId: 'codedx-api-key', variable: 'API_KEY'),
                    string(credentialsId: 'codedx-url', variable: 'CODEDX_URL'),
                    string(credentialsId: 'codedx-project-id', variable: 'PROJECT_ID')
                ])
                step([
                    $class: 'CodeDxPublisher',
                    analysisName: 'Build #${BUILD_NUMBER}',
                    key: "${API_KEY}",
                    projectId: "${PROJECT_ID}",
                    selfSignedCertificateFingerprint: '',
                    sourceAndBinaryFiles: '**',
                    url: "${CODEDX_URL}",
                    targetBranchName: "${BRANCH_NAME}",
                    baseBranchName: 'main'
                ])
            }
        }
    }
}
