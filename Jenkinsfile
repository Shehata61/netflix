pipeline{
    agent any
    tools{
        jdk 'jdk17'
        nodejs 'node16'
    }
    environment {
        SCANNER_HOME=tool 'sonar-scanner'
    }
    stages {
        stage('clean workspace'){
            steps{
                cleanWs()
            }
        }
        stage('Checkout from Git'){
            steps{
                git branch: 'main', url: 'https://github.com/Shehata61/netflix.git'
            }
        }
  

        stage("Docker Build & Push"){
            steps{
                script{
                   withDockerRegistry(credentialsId: 'docker', toolName: 'docker'){   
                       sh "docker build --build-arg TMDB_V3_API_KEY=7388e999dce9bd72d8a0bb287dc9ff3e -t netflix ."
                       sh "docker tag netflix naveen0101/netflix:latest "
                       sh "docker push naveen0101/netflix:latest "
                    }
                }
            }
        }
     
        stage('Deploy to container'){
            steps{
                sh 'docker run -d --name netflix -p 8081:80 naveen0101/netflix:latest'
            }
        }
    }
}
