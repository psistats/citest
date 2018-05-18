node {
    stage('prepare') {
        sh 'printenv'
    }
    stage('test-py35') {
        withPythonEnv('psikon-py35') {
            pysh 'pip install tox -vvv && tox -e py35'
        }
    }
    stage('test-py36') {
        withPythonEnv('psikon-py36') {
            pysh 'pip install tox && -vvv tox -e py36'
        }
    }
    stage('test-coverage') {
        withPythonEnv('psikon-py35') {
            pysh 'tox -e coverage'
            step([$class: 'CoberturaPublisher',
                autoUpdateHealth: false,
                autoUpdateStability: false,
                coberturaReportFile: 'coverage.xml',
                failUnhealthy: false,
                failUnstable: false,
                maxNumberOfBuilds: 30,
                onlyStable: true,
                sourceEncoding: 'utf-8',
                zoomCoverageCharge: true
            ])
        }
    }
}
