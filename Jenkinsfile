pipeline {
    agent any
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Vrushabh-gomai/ori_project.git'
            }
        }
        stage('Deploy to AWS CodeDeploy') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'aws-credentials', usernameVariable: 'AWS_ACCESS_KEY_ID', passwordVariable: 'AWS_SECRET_ACCESS_KEY')]) {
                    script {
                        sh '''
                        aws deploy create-deployment \
                        --application-name assignment_app \
                        --deployment-group-name assign_grp \
                        --github-location repository=Vrushabh-gomai/ori_project,commitId=$(git rev-parse HEAD) \
                        --region us-east-1
                        '''
                    }
                }
            }
        }
    }
}
