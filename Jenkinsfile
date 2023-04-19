pipeline {
    agent any
    stages {
        stage('Deploy backup on S3') {
            steps {
            // you need cloudbees aws credentials
            withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'jenkinscreds', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
                sh "cd /home/ubuntu/mysql_backup"
                sh "ll *.sql"
                
                sh "aws s3 cp $_ s3://mysqlbackup-idoc/"
            }
    }
    }
}
}


