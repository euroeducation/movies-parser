def imageName = 'euroeducation/movies-parser'
pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        def imageTest= docker.build("${imageName}-test", "-f Dockerfile.test .")

        stage('Quality Tests'){
            steps {
                script {
                    imageTest.inside{
                        sh 'golint'
                    }
                }
            }
        }

        stage('Unit Tests'){
            steps {
                script{
                    imageTest.inside{
                        sh 'go test'
                    }
                }
            }
        }
        
    }
}
