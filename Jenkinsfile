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
              withDockerRegistry{([credentialsId: "rushikesh8284", url: "https://hub.docker.com/repository/docker/rushikesh8284/devsecops"])
                   sh 'printenv'
                    sh 'sudo docker build -t rushi:""$GIT_COMMIT"" .'  
                    sh 'docker push localhost:5000/myfirstimage]:""$GIT_COMMIT""'

    }
}
