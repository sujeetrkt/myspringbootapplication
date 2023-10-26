pipeline{
agent any
tools{
    maven 'MAVEN'
}
    stages{
        stage('Build Maven Project '){
            steps{
                script{
                def myname=name;
                def dbname=db;
                echo "welcome to devops first step ${dbname} and ${myname}"
                }
               checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'b16f6603-da31-4566-89cd-d17d5a122f83', url: 'https://github.com/sujeetrkt/myspringbootapplication.git']])
                sh "mvn clean install"
            }

        }
    }


}
