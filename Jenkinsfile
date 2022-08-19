pipeline{
    agent any
    triggers{
        pollSCM('*/5 * * * *')
    }
    stages{
        stage('Build'){
            steps{
                sh 'mvn clean package'
            }
            post{
                success {
                    echo 'Arhiving....'
                    arhiveArtifacts artifacts:'**/target/*.war'
                }
            }
        }
        stage('Deployments')
            parallel{
                stage('Deploy to local'){
                    steps{
                        sh "cp **/target/*.war /home/dima/Загрузки/tomcat-local/webapps"
                    }
                }
                stage('Deplot to prod'){
                    steps{
                        sh "cp **/target/*.war /home/dima/Загрузки/tomcat-prod/webapps"
                    }
                }
            }
        }
    }
}
