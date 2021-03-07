
pipeline{
    agent any 
    stages{
        stage('Install  npm'){
            steps{
                sh "npm install"
            }
            post{
                always{
                    echo "Success Move to Var"
                }
                failure{
                    echo "fail operation Move to Var"
                    mail body: 'Error in Move to Var ', subject: 'Build failed!', to: 'kiadr9372@gmail.com'
                }
                success{
                 echo "Success Move to Var"
                }
            }
        }
        stage('Build Project'){
            steps{
                sh "ng build --prod "
            }
            post{
                always{
                    echo "Success Move to Var"
                }
                failure{
                    echo "fail operation Move to Var"
                    mail body: 'Error in Move to Var ', subject: 'Build failed!', to: 'kiadr9372@gmail.com'
                }
                success{
                 echo "Success Move to Var"
                }
            }
        }
        stage('Move to Var'){
            steps{
                sh "chown -R root:jenkins /var/lib/jenkins/workspace/Angular-CI-CD--Test_master/dist/ang-CICD/. && /var/www/html"
            }
            post{
                always{
                    echo "Success Move to Var"
                }
                failure{
                    echo "fail operation Move to Var"
                    mail body: 'Error in Move to Var ', subject: 'Build failed!', to: 'kiadr9372@gmail.com'
                }
                success{
                 echo "Success Move to Var"
                }
            }
        }
    }
}
