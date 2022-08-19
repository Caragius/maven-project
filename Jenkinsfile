pipeline{
    agent any
    triggers{
        pollSCM('*/1 * * * *')
    }
    stages{
        stage('Build'){
            steps{
                sh 'mvn clean package'
            }
            post{
                success {
                    echo 'Arhiving....'
                    archiveArtifacts artifacts:'**/target/*.war'
                }
            }
        }
        stage('Deployments'){
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
