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

        //Stage3 : Publish the artifacts to Nexus
        stage('Publish to Nexus'){
            steps{
                script {

                def NexusRepo = version.endsWith("SNAPSHOT") ? "DevopsLab-SNAPSHOT" : "DevOpsLab-RELEASE"

                nexusArtifactUploader artifacts:
                [[artifactId: "${ArtifactId}", 
                classifier: '', 
                file: "target/${ArtifactId}-${Version}.war", 
                type: 'war']], 
                credentialsId: '9028e13f-7ee4-4909-a2f3-f8cdbb0efb64', 
                groupId: "${GroupId}", 
                nexusUrl: '172.20.10.144:8081', 
                nexusVersion: 'nexus3', 
                protocol: 'http', 
                repository: "${NexusRepo}", 
                version: "${Version}"

                }
            }
        }

        //Stage4 : print the ENV variables
        stage ('Print the ENV variables'){
            steps {
                echo "Artifact ID is '${ArtifactId}'"
                echo "Version is '${Version}'"
                echo "GroupId is '${GroupId}'"
                echo "Name ID is '${Name}'"
            }

        }

    
        

        
        
    }

}