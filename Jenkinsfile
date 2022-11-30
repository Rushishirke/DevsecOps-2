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
        
             stage("Docker build"){ 
                steps{
                  sh 'docker version'
                  sh 'docker build -t devsecops .'
                  sh 'docker image list'
                  sh 'docker tag devsecops Rushikesh8284/rushi8284:devsecops'
                  withDockerRegistry{([(credentialsId: 'DOCKER_HUB_PASSWORD', url: '')]) 
                  sh 'docker push Rushikesh8284/devsecops:1.0'
                  }
            }
        }
             stage("Push Image to Docker Hub"){
                steps{
               sh 'docker push Rushikesh8284/rushi8284:devsecops'
            }
        
             
        }
    }
}      
    

