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

       stage("Docker build and push"){
            steps{
              withDockerRegistry{([credentialsId: "docker-ID", url: ""])
                   sh 'printenv'
                    sh 'sudo docker build -t rushi:""$GIT_COMMIT"" .'  
                    sh 'docker push rushi/numeric-app:""$GIT_COMMIT""'
              }
            }
        }

    }
}
