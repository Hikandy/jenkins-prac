pipeline {
    agent any
    triggers { pollSCM('* * * * *') }
    stages {
        stage('checkout') {
            steps {
                git url: 'https://github.com/Hikandy/spring-petclinic-jenkins.git', branch: 'main'
            }
        }    
        stage('build') {
            steps {
                sh "./mvnw clean package"
            }
            post {
                always {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                }
                changed {
                    emailext attachLog: true, 
                    body: 'Please go to ${BUILD_URL} and verify the build', 
                    compressLog: true, 
                    recipientProviders: [requestor()], 
                    to: "test@jenkins",
                    subject: '"Job \'${JOB_NAME}\' (${BUILD_NUMBER}) is waiting for input"'
                }
            }
        }
    }
}
    
