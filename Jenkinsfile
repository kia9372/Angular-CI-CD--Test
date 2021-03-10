
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
                stage('find with ls path')
                     {
                    steps {
                        sh 'ls'
                    }
                     }
                stage('upload ftp ')
                     {
                    steps {
                        // sh 'git ftp init --user lsendes1 --passwd K720228d ftp://193.141.64.96/public_html'
                        sh 'curl -T /var/lib/jenkins/workspace/Angular-CI-CD--Test_develop/dist/ang-CICD ftp://lsendes1:K720228d@193.141.64.96/public_html'
                    }
                     }
            }

                post {
                    always {
                        echo 'Start Upload to Server'
                    }
                    failure {
                        echo 'fail operation Move to Var'
                        // mail body: "${env.BUILD_URL} has result ${currentBuild.result}", subject: "Status of pipeline: ${currentBuild.fullDisplayName}", to: 'kiadr9372@gmail.com'
                        emailext attachLog: true, body:
                        """<p>EXECUTED: Job <b>\'${env.JOB_NAME}:${env.BUILD_NUMBER})\'
                        </b></p><p>View console output at "<a href="${env.BUILD_URL}">
                        ${env.JOB_NAME}:${env.BUILD_NUMBER}</a>"</p><p><i>(Build log is attached.)</i></p>""",
                        compressLog: true,
                        recipientProviders: [[$class: 'DevelopersRecipientProvider'],
                        [$class: 'RequesterRecipientProvider']],
                        replyTo: 'do-not-reply@company.com',
                        subject: "Status: ${currentBuild.result?:'SUCCESS'} - Job \'${env.JOB_NAME}:${env.BUILD_NUMBER}\'",
                        to: 'kiadr9372@gmail.com'
                    }
                    success {
                        echo 'Success Move to Var'
                    }
                }
            }
    }
}
