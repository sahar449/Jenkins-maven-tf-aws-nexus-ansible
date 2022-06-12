pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'
    }
    environment{
       ArtifactId = readMavenPom().getArtifactId()
       Version = readMavenPom().getVersion()
       Name = readMavenPom().getName()
       GroupId = readMavenPom().getGroupId()
    }
    stages {
        // Specify various stage with in stages

        // stage 1. Build
        stage ('Build'){
            steps {
                sh 'mvn clean install package'
            }
        }

        // Stage2 : Testing
        stage ('Test'){
            steps {
                echo ' testing......'

            }
        }

        // Stage3 : Publish the artifacts to Nexus
        stage ('Publish to Nexus'){
            steps {
                    nexusArtifactUploader artifacts: [[artifactId: "${ArtifactID}", classifier: '', file: "target/${ArtifactID}-${Version}.war", type: 'war']], credentialsId: '63948a7a-86eb-4912-bd54-29c345042e56', groupId: "${GroupID}", nexusUrl: '172.20.10.100:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'Release' , version: "${Version}"
            }            
        }
    }        
}     