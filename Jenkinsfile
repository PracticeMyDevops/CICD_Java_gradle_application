pipeline{
    agent any
    stages{
        stage("sonar quality check"){
            agent{
                docker{
                    args '-u root'
                    image 'openjdk:11'
                    
                }
            }
            steps{
                script{
                    withSonarQubeEnv(credentialsId: 'sonar-token') {
                        sh 'chmod +x gradlew'
                        sh './gradlew sonarqube'
                    }
                }
            }
        }
    }
}
