pipeline {
    agent { label 'LINUX'}
    
    stages {
        stage('Version Control System') {
            steps {
                git url: 'https://github.com/krishna6788/spring-petclinic.git',
                    branch: 'Declrative'

            }
        }
        
        stage('SonarQube analysis') {
            steps {
                withSonarQubeEnv('SONAR_ENV')
                sh 'mvn clean install sonar:sonar -Dsonar.organization=spc-decl -Dsonar.token=1316fa3ba82b3fa5d6f3544ac726bed4aa26d542 -Dsonar.projectKey=spc-decl'
            }
    }
        stage('Post Build') {
            steps {
                archiveArtifacts artifacts: '**/target/spring-petclinic-3.0.0-SNAPSHOT.jar',
                   allowEmptyArchive: true,
                   fingerprint: true,
                   onlyIfSuccessful: true
            junit testResults: '**/target/surefire-reports/TEST-*.xml'


            }
            
            
        }
    }
}