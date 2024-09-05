pipeline {
    agent any
    environment {
        AWS_ACCESS_KEY_ID_CRED = credentials('aws-access-key-id')  // ID for the AWS Access Key
        AWS_SECRET_ACCESS_KEY_CRED = credentials('Secret access key')  // ID for the AWS Secret Key
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
                    aws deploy create-deployment \
                        --application-name assignment_app \
                        --deployment-group-name assign_grp \
                        --github-location repository=Vrushabh-gomai/ori_project,commitId=$(git rev-parse HEAD) \
                        --region us-west-2 \
                        --access-key-id ${AWS_ACCESS_KEY_ID_CRED} \
                        --secret-access-key ${AWS_SECRET_ACCESS_KEY_CRED}
                    '''
                }
            }
        }
    }
}



