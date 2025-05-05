pipeline{

    agent any

    environment {
        AWS_REGION = 'ap-south-1' // Change to your region
        AWS_CREDENTIALS_ID = '415007686326' // ID of Jenkins stored credentials
        GIT_URL = "https://github.com/2507Teju/EC2-Projects.git"
    }

    triggers{
        cron('H/2 * * * *')
    }

    stages{
        stage('Chekout'){
            steps{
                url : ${env.GIT_URL}
            }
        }
        stage('Create EC2 Snapshot'){
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