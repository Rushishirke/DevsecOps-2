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
              sh "mvn test-1"
            }
        }

       

    }
}
