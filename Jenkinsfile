
pipeline {
    triggers {
        pollSCM('*/1 * * * * ')
    }
    agent any
    stages {
        parallel{
            stage('check out source manager') {
                steps {
                    checkout scm
                }
            }
            stage('Install  npm') {
                steps {
                    sh 'npm install'
                }
                post {
                    always {
                        echo 'Success npm install'
                    }
                    failure {
                        echo 'fail operation npm installr'
                        mail body: 'Error in npm install ', subject: 'Build failed!', to: 'kiadr9372@gmail.com'
                    }
                    success {
                        echo 'Success npm install'
                    }
                }
            }
            stage('Build Project Develop') {
                when {
                    branch 'develop'
                }
                steps {
                    sh 'ng build --prod '
                }
                post {
                    always {
                        echo 'Success Build Project'
                    }
                    failure {
                        echo 'fail operation Build Project'
                        mail body: 'Error in Build Project ', subject: 'Build failed!', to: 'kiadr9372@gmail.com'
                    }
                    success {
                        echo 'Success Build Project'
                    }
                }
            }
            stage('Build Project Realase') {
                when {
                    branch 'master'
                }
                steps {
                    sh 'ng build --prod '
                }
                post {
                    always {
                        echo 'Success Build Project'
                    }
                    failure {
                        echo 'fail operation Build Project'
                        mail body: 'Error in Build Project ', subject: 'Build failed!', to: 'kiadr9372@gmail.com'
                    }
                    success {
                        echo 'Success Build Project'
                    }
                }
            }
            stage('Move to Var') {
                steps {
                    sh 'chown -R root:jenkins /var/lib/jenkins/workspace/Angular-CI-CD--Test_master/dist/ang-CICD/. && /var/www/html'
                }
                post {
                    always {
                        echo 'Success Move to Var'
                    }
                    failure {
                        echo 'fail operation Move to Var'
                        mail body: 'Error in Move to Var ', subject: 'Build failed!', to: 'kiadr9372@gmail.com'
                    }
                    success {
                        echo 'Success Move to Var'
                    }
                }
            }
        }
        
    }
}
