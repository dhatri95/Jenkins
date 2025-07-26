pipeline {
    agent {
        label 'Node-1'
    }

    parameters {
        string(name: 'APP_NAME', defaultValue: 'MyApp', description: 'Name of the application')
        choice(name: 'ENV', choices: ['dev', 'qa', 'prod'], description: 'Deployment environment')
        booleanParam(name: 'RUN_TESTS', defaultValue: true, description: 'Run tests after build')
    }

    options {
        timeout(time: 10, unit: 'MINUTES')  // Limits pipeline execution time
        disableConcurrentBuilds()  // Prevents overlapping runs
    }

    stages {
        stage('Build') {
            steps {
                echo "Building ${params.APP_NAME} for ${params.ENV} environment..."
                sh 'echo "Build step executed."'
            }
        }

        stage('Test') {
            when {
                expression { return params.RUN_TESTS }
            }
            steps {
                echo 'Running tests...'
                sh 'echo "Tests executed."'
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying ${params.APP_NAME} to ${params.ENV}..."
                sh 'echo "Deployment step executed."'
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline completed successfully!'
        }
        failure {
            echo '❌ Pipeline failed. Check logs for details.'
        }
        always {
            echo '📦 Cleaning up...'
            cleanWs()
        }
    }
}
