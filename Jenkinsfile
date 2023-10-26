pipeline{
    agent any
    
    tools{
        maven 'MAVEN'
    }
      environment {
        NEXUS_VERSION = "nexus3"
        NEXUS_PROTOCOL = "http"
        NEXUS_URL = "localhost:8081"
        NEXUS_REPOSITORY = "maven-central-repository"
        NEXUS_CREDENTIAL_ID = "NEXUS_CRED"
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
        stage("Publish to Nexus Repository Manager") {
        steps{
            script {
                   pom = readMavenPom file: "pom.xml";
                    filesByGlob = findFiles(glob: "target/*.${pom.packaging}");
                    echo "${filesByGlob[0].name} ${filesByGlob[0].path} ${filesByGlob[0].directory} ${filesByGlob[0].length} ${filesByGlob[0].lastModified}"
                    artifactPath = filesByGlob[0].path;
                    artifactExists = fileExists artifactPath;
                    if(artifactExists) {
                        echo "*** File: ${artifactPath}, group: ${pom.groupId}, packaging: ${pom.packaging}, version ${pom.version}";
                        nexusArtifactUploader(
                            nexusVersion: NEXUS_VERSION,
                            protocol: NEXUS_PROTOCOL,
                            nexusUrl: NEXUS_URL,
                            groupId: 'pom.com.in28minutes.rest.webservices',
                            version: 'pom.2.1.7-RELEASE',
                            repository: NEXUS_REPOSITORY,
                            credentialsId: NEXUS_CREDENTIAL_ID,
                            artifacts: [
                                [artifactId: 'pom.01-hello-world-rest-api',
                                classifier: '',
                                file: artifactPath,
                                type: pom.packaging],
                                [artifactId: 'pom.01-hello-world-rest-api',
                                classifier: '',
                                file: "pom.xml",
                                type: "pom"]
                            ]
                        );
                    } else {
                        error "*** File: ${artifactPath}, could not be found";
                    }
            }
        }
        }
         stage('Build maven Docker Image') {
            steps {
                script {
                  bat 'docker build -t sujeetrkt/hello-world-rest-api .'
                }
            }
        }
         stage('Deploy Docker Image to DockerHub') {
            steps {
                script {

                    withCredentials([string(credentialsId: 'DOCKER_HUB_PWD', variable: 'dockerhubpwd')]) {
 bat 'docker login -u sujeetcog@gmail.com -p ${dockerhubpwd}'
  bat 'docker push sujeetrkt/hello-world-rest-api'
}
           
        }
            }   
        }
    }
}
