pipeline {
    agent any
    
    environment {
        BUCKET_NAME = 'mysqlbackup-idoc'
        BACKUP_FOLDER = '/home/ubuntu/mysql_backup/'
    }
    
    stages {
        stage('Creating Backup of Database'){
            steps{
                sh "/opt/jenkins_scripts/mysql_backup.sh"
            }
        }
        stage('Find backup file') {
            steps {
                script {
                    def backupFile = sh(returnStdout: true, script: "ls -1 ${env.BACKUP_FOLDER}*.sql | tail -n 1").trim()
                    if (backupFile) {
                        println "Found backup file: ${backupFile}"
                        env.BACKUP_FILE = backupFile
                    } else {
                        error "No backup file found in ${env.BACKUP_FOLDER}"
                    }
                }
            }
        }
        
        stage('Upload backup to S3') {
            steps {
                withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'jenkinscreds', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
                    sh "aws s3 cp ${env.BACKUP_FILE} s3://${env.BUCKET_NAME}/"
                }
            }
        }
    }
}
