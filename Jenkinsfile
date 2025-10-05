pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = 'us-east-1'
        S3_BUCKET = 'your-s3-bucket-name'
    }

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/Yashvrm74/static-website.git'
            }
        }

        stage('Deploy to S3') {
            steps {
                sh '''
                aws s3 sync . s3://$S3_BUCKET --acl public-read
                '''
            }
        }

        stage('Verify Website') {
            steps {
                sh '''
                curl http://$S3_BUCKET.s3-website-$AWS_DEFAULT_REGION.amazonaws.com
                '''
            }
        }
    }
}
