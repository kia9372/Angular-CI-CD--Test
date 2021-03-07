
pipeline{
    agent any 
    stages{
        stage('Install npm'){
            steps{
                sh "npm install"
            }
        }
        stage('Build Project'){
            steps{
                sh "ng build --prod "
            }
        }
        stage('Move to Var'){
            steps{
                sh "cp -a /var/lib/jenkins/workspace/Angular-CI-CD--Test_master/dist/ang-CICD/. /var/www/html"
            }
        }
    }
}
