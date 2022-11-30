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
                  sh 'docker tag devsecops rushikesh8284/rushi828:devsecops'
                  sh 'org.jenkinsci.plugins.plaincredentials.StringCredentials'([string(credentialsId: 'DOCKER_HUB_PASSWORD', variable: 'PASSWORD')]) {
                  sh 'docker login -u rushikesh8284 -p Rushi@123'
                  }
            }
        }
             stage("Push Image to Docker Hub"){
                steps{
               sh 'docker push rushikesh8284/rushi8284:devsecops'
            }
        
        
             
        }
    }
}      
    

