
pipeline{
    agent any 
    triggers {
        githubPush()
    }
    stages{
        stage('Install  npm'){
            steps{
                sh "npm install"
            }
            post{
                always{
                    echo "Success npm install"
                }
                failure{
                    echo "fail operation npm install"
                    mail body: 'Error in npm install ', subject: 'Build failed!', to: 'kiadr9372@gmail.com'
}
                }
                success{
                 echo "Success npm install"
                }
            }
        }
        stage('Build Project'){
            steps{
                sh "ng build --prod "
            }
            post{
                always{
                    echo "Success ng Build"
                }
                failure{
                    echo "fail operation ng Build"
                    mail body: 'Error in ng Build ', subject: 'Build failed!', to: 'kiadr9372@gmail.com'
}
                }
                success{
                 echo "Success ng Build"
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
                }
                success{
                 echo "Success Move to Var"
                }
            }
        }
    }
}
