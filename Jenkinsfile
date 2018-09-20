pipeline {
    agent any

    parameters {
        string(name: 'tomcat_local_dev', defaultValue: 'localhost', description: 'Staging Server')
        string(name: 'tomcat_aws_prod', defaultValue: '172.31.23.201', description: 'Production Server')
    }

    triggers {
        pollSCM('H/2 * * * *')
    }

    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }

            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage('Deployments') {
            parallel {
                stage('Deploy to Staging') {
                    steps {
                        sh "cp **/target/*.war /opt/tomcat-staging/webapps"

                    }
                }
                stage('Deploy to AWS Production') {
                    steps {
                        sh "scp -i /home/jenkins/tomcat-demo.pem **/target/*.war ec2-user@${params.tomcat_aws_prod}:/var/lib/tomcat7/webapps"

                    }
                }
            }
        }

    }

}