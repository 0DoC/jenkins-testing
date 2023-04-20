pipeline {
    agent any
    stages {
        stage('Deploy backup on S3') {
            steps {
            // you need cloudbees aws credentials
            withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'jenkinscreds', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
                script {
                    script {
                        POM_VERSION = sh(script: '/bin/bash -c \'mysqlpath=$(ls -al /home/ubuntu/mysql_backup/*.sql | awk \'{print $9}\'\') && aws s3 cp $mysqlpath s3://mysqlbackup-idoc/\'', returnStdout: true)
                        echo "${POM_VERSION}"
                    }
                }
            }
    }
    }
}
}

