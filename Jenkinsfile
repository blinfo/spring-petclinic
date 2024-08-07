pipeline {
    agent {
        label 'linux'
    }
    options {
        disableConcurrentBuilds()
    }
    environment {
        QODANA_TOKEN = credentials('d5b8a737-8e25-4dde-ab7e-95e7cb862da7')
        GITHUB_REPO_NAME = 'spring-petclinic'
    }
    stages {
        stage('Qoadana Code Analysis') {
            agent {
                docker {
                    args '''
               -v "${WORKSPACE}":/data/project
               --entrypoint=""
               '''
                    image 'jetbrains/qodana-jvm:latest'
                    reuseNode true
                }
            }
            steps {
                sh '''qodana -save-report --fail-threshold 0'''
//                 sh 'docker run -v $(pwd):/data/project/ -e QODANA_TOKEN=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJvcmdhbml6YXRpb24iOiJBTjRWdyIsInByb2plY3QiOiIzZWV5NSIsInRva2VuIjoiM3drODEifQ.D_DA1IO8_o_92gMXTbcSdALakSYWGINmffgRGf5LzvQ jetbrains/qodana-jvm:latest'
            }
        }
    }
}
