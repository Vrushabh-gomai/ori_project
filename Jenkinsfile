pipeline {
    agent any
    environment {
        AWS_ACCESS_KEY_ID = 'your-access-key-id'  // Replace with your actual AWS access key
        AWS_SECRET_ACCESS_KEY = 'your-secret-access-key'  // Replace with your actual AWS secret key
    }
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Vrushabh-gomai/ori_project.git'
            }
        }
        stage('Deploy to AWS CodeDeploy') {
            steps {
                script {
                    sh '''
                    export AWS_ACCESS_KEY_ID=${AWS_ACCESS_KEY_ID}
                    export AWS_SECRET_ACCESS_KEY=${AWS_SECRET_ACCESS_KEY}
                    
                    aws deploy create-deployment \
                    --application-name assignment_app \
                    --deployment-group-name assign_grp \
                    --github-location repository=Vrushabh-gomai/ori_project,commitId=$(git rev-parse HEAD) \
                    --region us-west-2
                    '''
                }
            }
        }
    }
}
