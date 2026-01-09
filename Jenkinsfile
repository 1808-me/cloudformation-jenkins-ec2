pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = 'us-east-1'
        STACK_NAME = 'ec2-jenkins-stack'
    }

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Deploy CloudFormation Stack') {
            steps {
                withAWS(credentials: 'aws-access-key', region: "${AWS_DEFAULT_REGION}") {
                    bat '''
                    aws cloudformation deploy \
                      --template-file template.yaml \
                      --stack-name $STACK_NAME \
                      --parameter-overrides KeyName=my-keypair \
                      --capabilities CAPABILITY_NAMED_IAM
                    '''
                }
            }
        }
    }
}
