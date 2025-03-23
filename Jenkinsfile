pipeline {
    agent {
        docker {
            image 'conanio/gcc10'
            args "-u root"
        }
    }
    environment {
        BUILD_DIR = 'build'
    }
    options {
        workspace('/workspace')
    }
    stages {
        stage('Checkout') {
            steps {
                git credentialsId: 'gitlab-credentials-id',
                    url: 'https://github.com/B1lok/lab4-GL.git',
                    branch: 'main'
            }
        }
        stage('Build') {
            steps {
                sh 'cmake -S . -B ${BUILD_DIR}'
                sh 'cmake --build ${BUILD_DIR}'
            }
        }
        stage('Test') {
            steps {
                sh './${BUILD_DIR}/vs_mkr_test1 --gtest_output=xml:report.xml'
            }
            post {
                always {
                    junit 'report.xml'
                }
            }
        }
    }
    post {
        success {
            echo 'Build and tests were successful!'
        }
        failure {
            echo 'Something went wrong!'
        }
    }
}
