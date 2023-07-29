pipeline {
    agent { label 'LINUX'}
    parameters {
        parameters(name:'MAVEN_GOAL', defaultValue: 'package', description: 'maven goal')
    }
    stages {
        stage('Version Control System') {
            steps {
                git url 'https://github.com/krishna6788/spring-petclinic.git'
                    branch 'Declrative'

            }
        }
        stage('Building') {
            steps {
                sh "mvn ${params.MAVEN_GOAL}"

            }
        }
        stage('Post Build') {
            
            archiveArtifacts artifacts: '****/target/spring-petclinic-3.0.0-SNAPSHOT.jar',
                   allowEmptyArchive: true,
                   fingerprint: true,
                   onlyIfSuccessful: true
            junit testResults: '**/target/surefire-reports/TEST-*.xml'

        }
    }
}