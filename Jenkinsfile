pipeline {
    agent any

    environment{
        NETLIFY_SITE_ID = '37eb0861-de7f-4809-a01f-edbe442d6962'
        NETLIFY_AUTH_TOKEN = credentials('netlify-token')
        REACT_APP_VERSION = "1.0.$BUILD_ID"
        AWS_DEFAULT_REGION = 'us-east-1'
    }
    
    stages {

        stage('Deploy to AWS') {
            agent {
                docker {
                    image 'amazon/aws-cli'
                    reuseNode true
                    args "--entrypoint=''"
                }
            }
           
            steps {
                withCredentials([usernamePassword(credentialsId: 'my-aws', passwordVariable: 'AWS_SECRET_ACCESS_KEY', usernameVariable: 'AWS_ACCESS_KEY_ID')]) {
                    // some block
                    sh '''
                    aws --version
                    aws ecs register-task-definition --cli-input-json file://aws/task-defenition-prod.json
                    aws ecs update-service --cluster LearnJenkinsApp-Cluster-Prod --service LearnJenkinsApp-TaskDefenition-Prod --task-definition LearnJenkinsApp-TaskDefinition-Prod:1 
                    '''
                    
                }
                
            }
        }
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    ls -la
                    node --version
                    npm --version
                    npm ci
                    npm run build
                    ls -la
                '''
            }
        }
        
        
    }
}