pipeline {
    agent any
    stages {
        stage('Build Docker') {
            when { branch 'master' }
            steps {
                script {
                    docker.image('jekyll/jekyll').inside{
                        sh 'bundle install'                        
                        sh 'jekyll build'
                        sh 'ls'
                    }
                }
            }
        }
        
        stage('Upload S3') {
            steps {
                script {
                    withAWS(region: 'ap-southeast-1', credentials: 'aws-docs-staging') {
                        files = s3FindFiles(bucket:'docs-staging.katalon.com')
                        println files.length
                    }
                }
            }
        }
    }
}
