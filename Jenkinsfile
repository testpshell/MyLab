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

        //Stage3 : Publish the artifacts to Nexus
        stage('Publish to Nexus'){
            steps{
                nexusArtifactUploader artifacts: [[artifactId: 'DevOpsLab', classifier: '', file: 'target/DevOpsLab-0.0.5-SNAPSHOT.war', type: 'war']], credentialsId: '9028e13f-7ee4-4909-a2f3-f8cdbb0efb64', groupId: 'com.devopslab', nexusUrl: '172.20.10.144:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'DevopsLab-SNAPSHOT', version: '0.0.5-SNAPSHOT'
            }
        }

        //Stage4 : print the ENV variables
        stage ('Print the ENV variables'){
            steps {
                echo "Artifact ID is '${ArtifactId}'"
                echo "Version is '${Version}'"
                echo "Name ID is '${Name}'"
            }

        }

    
        

        
        
    }

}