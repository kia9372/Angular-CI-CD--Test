
pipeline{
    agent any 
    stages{
        stage('Install npm){
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
                sh "mv dist/ang-cicd/* /var/www/html"
            }
        }
    }
}
