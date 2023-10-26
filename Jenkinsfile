pipeline{
agent any
tools{
    maven 'MAVEN'
}
    stages{
        stage('Build Maven Project '){
            steps{
             checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/sujeetrkt/myspringbootapplication.git']])
               sh "mvn clean package" 
            }

        }
    }


}
