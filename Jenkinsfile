pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = 'us-east-1'
        S3_BUCKET = 'websitestack-websitebucket-apnzrbuy7m9o'
    }

    stages {
        stage('Clone Repo') {
            steps {
                echo 'Cloning the main branch from GitHub...'
                git branch: 'main', url: 'https://github.com/Yashvrm74/static-website.git'
            }
        }

        stage('Deploy to S3') {
            steps {
                echo "Deploying website files to S3 bucket: ${S3_BUCKET}"
                sh '''
                aws s3 sync . s3://$S3_BUCKET --acl public-read
                '''
            }
        }

        stage('Verify Website') {
            steps {
                echo "Verifying website..."
                sh '''
                curl http://$S3_BUCKET.s3-website-$AWS_DEFAULT_REGION.amazonaws.com
                '''
            }
        }
    }

    post {
        success {
            echo "✅ Website deployed successfully!"
        }
        failure {
            echo "❌ Deployment failed. Check logs above."
        }
    }
}
