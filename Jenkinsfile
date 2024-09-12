pipeline{
    agent any
    tools{
        maven "MAVEN3"
        jdk "OracleJDK8"
    }

    environment{
        NEXUS_GRP_REPO = 'vprofile-maven-group'
        NEXUSIP = '172.31.88.37'
        NEXUSPORT = '8081'

        SNAP_REPO = 'vprofile-snapshot'
        RELEASE_REPO = 'vprofile-release'
        CENTRAL_REPO = 'vprofile-maven-central'

        NEXUS_USER = 'admin'
        NEXUS_PASS = 'admin123'

    }

    stages {
        stage('Build'){
            steps{
                sh 'mvn -s settings.xml -DskipTests install'
            }
            
            post{
                sucess{
                    echo "Now Archiving."
                    archiveArtifacts artifacts: '**/*.war'
                }

            }
        }

        stage('Test'){
            steps{
                sh 'mvn -s settings.xml test'
            }
        }


        stage('Checkstyle Analysis'){
            steps{
                sh 'mvn -s settings.xml checkstyle:checkstyle' 
            }
        }

    }



}