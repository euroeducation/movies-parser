def imageName = 'euroeducation/movies-parser'
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
                    def imageTest= docker.build("${imageName}-test", "-f Dockerfile.test .")
                    imageTest.inside{
                        sh 'golint'
                    }
                }
            }
            
        }
    }
}