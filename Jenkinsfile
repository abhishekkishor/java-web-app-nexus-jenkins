node{
    
    stage("Git Clone") {
        
        git url: 'https://github.com/abhishekkishor/java-web-app-nexus-jenkins.git', branch:'master'
        
    }
    
    stage("Maven Build"){
        
        sh "mvn clean package"
        
        archiveArtifacts artifacts: '**/*.war'
        
    }
    
    stage("Nexus Repo") {
        
        def readPom = readMavenPom 'pom.xml'

        nexusArtifactUploader artifacts: [
            [
                artifactId: 'java-web-app',
                classifier: '',
                file: "target/java-web-app-${readPom.version}.war",
                type: 'war'
            ]
        
        ],
                
        credentialsId: 'nexus3', 
        groupId: 'com.mt', 
        nexusUrl: '172.31.8.152:8081', 
        nexusVersion: 'nexus3', 
        protocol: 'http', 
        repository: 'jenkins-nexus',
        version: "${readPom.version}"
        
    }
    
}