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
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: '6f614f89-cb70-4678-a744-07109e61f147', url: 'https://github.com/sujeetrkt/myspringbootapplication.git']])
                sh "mvn clean install"
            }

        }
    }


}
