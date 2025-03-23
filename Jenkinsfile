pipeline {
    agent {
        docker {
            image 'conanio/gcc10'
            args "--user root -v ${env.WORKSPACE}:/workspace:rw -w /workspace"
        }
    }
    environment {
        BUILD_DIR = 'build'
    }
    stages {
        stage('Checkout') {
            steps {
                git credentialsId: 'gitlab-credentials-id',
                    url: 'https://github.com/B1lok/lab4-GL.git',
                    branch: 'main'
                sh 'ls -la ${env.WORKSPACE}'
            }
        }
        stage('Build') {
            steps {
                sh 'ls -la /workspace'
                sh 'cmake -S /workspace -B /workspace/${BUILD_DIR}'  
                sh 'cmake --build /workspace/${BUILD_DIR}'
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
