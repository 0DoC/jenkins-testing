pipeline {
    agent any 
    stages {
        stage('Deploy backup on S3') {
            steps {
            // you need cloudbees aws credentials
            withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'jenkinscreds', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
                sh "aws s3 ls"
                sh "aws s3 cp /home/ubuntu/mysql_backup/*.sql s3://mysqlbackup-idoc/"
            }
    }
    }
}
}
