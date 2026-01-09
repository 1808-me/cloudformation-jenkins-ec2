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
                withAWS(credentials: 'aws-credentials-id', region: env.AWS_DEFAULT_REGION) {
                    bat "\"C:\\Program Files\\Amazon\\AWSCLI\\bin\\aws.exe\" cloudformation deploy " +
                        "--template-file template.yaml " +
                        "--stack-name ${env.STACK_NAME} " +
                        "--parameter-overrides KeyName=my-keypair " +
                        "--capabilities CAPABILITY_NAMED_IAM"
                }
            }
        }
    }
}

