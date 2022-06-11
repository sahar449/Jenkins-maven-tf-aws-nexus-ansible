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
        // Stage3: Upload to Nexus
        stage ('upload to nexus'){
            steps {
                nexusArtifactUploader artifacts: [[artifactId: 'VinayDevOpsLab', classifier: '', file: 'target/VinayDevOpsLab-0.0.8.war', type: 'war']], credentialsId: '63948a7a-86eb-4912-bd54-29c345042e56', groupId: ${GroupId}", nexusUrl: '172.20.10.100:8081', nexusVersion: 'nexus3', protocol: 'http', repository: "${NexusRepo}", version: "${Version}"
            }
        }        
	    stage ('Print env variable') {
		    steps{
			    echo "Artifact ID is '${ArtifactID}'"
			    echo "Version is '${Version}'"
			    echo "Group ID is '${GroupID}'"
			    echo "Name is '${Name}'"
			}
	}
}