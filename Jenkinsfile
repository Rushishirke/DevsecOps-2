pipeline{
    agent(any)
    stages{
        stage("Build Artifact"){
            steps{
              sh "mvn clean package -DskipTests=true"
              archiveArtifacts 'target/*.jar' //so that they can be downloaded later
            }
        }

        stage("Jacoco test"){
            steps{
              sh "mvn test"
            }
        }
            stage('Mutation Tests - PIT') {
             steps {
                sh "mvn org.pitest:pitest-maven:mutationCoverage"
            }
        }
        stage("sonarqube"){
            steps{
                sh "sonarqube analysis"
            }
        }
        stage("Docker build"){ 
            steps{
              sh 'docker version'
              sh 'docker build -t devsecops .'
              sh 'docker image list'
              sh 'docker tag devsecops rushikesh8284/rushi828:devsecops'
              withCredentials([string(credentialsId: 'DOCKER_HUB_PASSWORD', variable: 'PASSWORD')]) {
              sh 'docker login -u rushikesh8284 -p Rushi@123'
                  }
            }
        }
             
    }
}      
    

