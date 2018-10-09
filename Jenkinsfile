#!groovy
pipeline {
    agent any

    node {
        parameters {
        string(name: 'tomcat_local_dev', defaultValue: 'localhost', description: 'Staging Server')
        string(name: 'tomcat_aws_prod', defaultValue: '18.188.94.188', description: 'Production Server')
        }

        triggers {
            pollSCM('H * * * *')
        }

        def props = readProperties file: './config/test.properties'
        stages {
            stage('Notification') {
                steps {
                    parrallel (
                        line : {
                            echo 'token: props.LineToken'
                        },
                        slack: {

                        }
                    )
                }
            }

        }
    }
    

}
