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
                
            }

        }
    }


}
