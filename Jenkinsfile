#!groovy
def props = readProperties file: 'config/test.properties'
pipeline {
    agent any

    parameters {
        string(name: 'tomcat_local_dev', defaultValue: 'localhost', description: 'Staging Server')
        string(name: 'tomcat_aws_prod', defaultValue: '18.188.94.188', description: 'Production Server')
    }

    triggers {
        pollSCM('H * * * *')
    }

    
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
