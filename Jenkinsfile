
pipeline{
    agent any
    tools{
        maven 'MAVEN'
    }
    stages{
        stage("SCM Checkout"){
            steps{
           checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/sujeetrkt/myspringbootapplication.git']])
            }
        }
        stage("Maven Build"){
            steps{
                bat 'mvn clean install'
            }
        }
    }
}
