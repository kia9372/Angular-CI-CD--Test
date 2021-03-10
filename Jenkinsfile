
pipeline {
    triggers {
        pollSCM('*/1 * * * * ')
    }
    agent any
    stages {
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
                parallel {
                    stage('build') {
                        steps {
                            sh 'ng build --prod '
                        }
                    }
                stage('build B') {
                        steps {
                            echo 'hi'
                        }
                }
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
            stage('Uplod to server') {
            parallel {
                stage('find path')
                     {
                    steps {
                        sh 'ls'
                    }
                     }
                stage('upload ftp ')
                     {
                    steps {
                        // sh 'git ftp init --user lsendes1 --passwd K720228d ftp://193.141.64.96/public_html'
                        sh 'curl -T ./dis/ang-CICD/ ftp://lsendes1:K720228d@FQDN/public_html'
                    }
                     }
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
