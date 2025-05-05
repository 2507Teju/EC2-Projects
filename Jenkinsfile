pipeline{

    agent any

    environment {
        AWS_REGION = 'ap-south-1'
        AWS_CREDENTIALS_ID = 415007686326 
    }

    triggers{
        cron('H/5 * * * *')
    }

    stages{
        stage('Create EC2 Snapshot'){
            agent{
                label 'slave3'
            }
            steps{
                withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: "${env.AWS_CREDENTIALS_ID}"]]) {
                    sh '''
                        aws ec2 create-snapshot --volume-id vol-0a7ac2f49fb2eaeec --description "Snapshot of the root volume for i-0d67b8844817d4c3a"

                    '''
            }
        }
    }
    }

    post{
        success{
            echo "Snapshot created successfully"
        }
        failure{
            echo "Snapshot creation failed"
        }
    }


}