pipeline {
    agent any

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
            }
        }
    }
}
    
