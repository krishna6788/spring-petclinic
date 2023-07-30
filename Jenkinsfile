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
                withSonarQubeEnv('Sonar') {
                sh 'mvn clean install sonar:sonar -Dsonar.organization=spc-decl -Dsonar.host.url=https://sonarcloud.io -Dsonar.token=ad034bdbcdc6f595e63a69b0a0bf57a19c956b4f -Dsonar.projectKey=spc-decl'
            }
        }
        }
        stage('Post Build') {
            steps {
                archiveArtifacts artifacts: '**/target/spring-*.jar',
                   allowEmptyArchive: true,
                   fingerprint: true,
                   onlyIfSuccessful: true
            junit testResults: '**/target/surefire-reports/TEST-*.xml'


            }
            
            
        }
    }
}