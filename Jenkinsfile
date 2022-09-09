pipeline {
    agent { docker { image 'maven:3.8.4-openjdk-11-slim' } }
    stages {
        stage('build') {
            steps {
                sh 'mvn --version'
            }
        }
        stage('nexus'){
            steps {
                script {
                    //pipeline-utility-steps
                        def pom = readMavenPom file: "pom.xml";
                        
                    dir("target"){
                        nexusArtifactUploader{
                            nexusVersion: 'nexus3',
                            protocol: 'http',
                            nexusUrl: 'http://localhost:8081/repository/app-init/'
                            groupId: pom.groupId,
                            version: pom.version,
                            repository: 'app-init'
                            credentialsId: 'nexuscredenciales'
                            artifacts: [
                                [artifactId: pom.artifactId,
                                 classifier: '',
                                 file: '',
                                 type: pom.packaging]
                                ]
                            )
                        }
                    }
                }
            }
        }                  
    }
}
