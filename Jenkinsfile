pipeline{
    agent any
    environment{
        VERSION ="${env.BUILD_ID}"
    }
    stages{
        stage("sonar quality check"){
            steps{
                script{
                    withSonarQubeEnv(credentialsId: 'Sonar Token') {
                        sh 'chmod +x gradlew'
                        sh './gradlew sonarqube'
                    }
                }
            }
        }
    stage("docker build & docker push"){
        steps{
            script{
                withCredentials([string(credentialsId: 'docker_pass', variable: 'docker_pass')]) {
                    sh '''
                    sudo docker build -t 34.125.174.235:8083/springapp:${VERSION} .
                    sudo docker login -u admin -p -S $docker_pass 34.125.174.235:8083
                    sudo docker push 34.125.174.235:8083/springapp:${VERSION}
                    sudo docker rmi 34.125.174.235:8083/springapp:${VERSION}
                    '''
                }
                
            }
        }
    }
    }

}
