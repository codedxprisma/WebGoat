pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                withCredentials([
                    string(credentialsId: 'API_KEY', variable: 'API_KEY'),
                    string(credentialsId: 'CODEDX_URL', variable: 'CODEDX_URL'),
                    string(credentialsId: 'PROJECT_ID', variable: 'PROJECT_ID')
                ]) {
                    step([
                        $class: 'CodeDxPublisher',
                        analysisName: 'Build #${BUILD_NUMBER}',
                        key: "${API_KEY}",
                        projectId: "${PROJECT_ID}",
                        selfSignedCertificateFingerprint: '',
                        sourceAndBinaryFiles: '',
                        url: "${CODEDX_URL}",
                        targetBranchName: '${BRANCH_NAME}',
                        baseBranchName: 'main',
                        gitFetchConfiguration: [specificBranch: '${BRANCH_NAME}'],
                        analysisResultConfiguration: [
                            failureOnlyNew: false,
                            failureSeverity: 'None',
                            numBuildsInGraph: 0,
                            policyBreakBuildBehavior: 'MarkFailed',
                            unstableOnlyNew: false,
                            unstableSeverity: 'None'
                        ]
                    ])
                }
            }
        }
    }
}
