def imageName = 'euroeducation/movies-parser'
def imageTest= ''
pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        

        stage('Quality Tests'){
            steps {
                script {
                    imageTest= docker.build("${imageName}-test", "-f Dockerfile.test .")
                    imageTest.inside{
                        sh 'golint'
                        sh 'go test'
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
