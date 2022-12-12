node{
    
    stage("Git Clone") {
        
        echo "==================================Pulling Application Code======================================"
        
        git url: 'https://github.com/abhishekkishor/java-web-app-nexus-jenkins.git', branch:'master'
        
        echo "==================================Application Code Pulled======================================="
        
    }
    
    stage("Maven Build"){
        
        echo "=====================================Building Maven Package========================================"
        
        sh "mvn clean package"
        
        echo "==================================Maven Package Built (WAR)========================================"
        
    }
    
    stage("Archiving Artifact"){
        
        echo "======================================Archiving Artifact========================================="
        
        archiveArtifacts artifacts: '**/*.war'
        
        echo "======================================Artifact Archived========================================="
    }

    stage("Nexus Repo") {
        
        def readPom = readMavenPom file: 'pom.xml'
        
        echo "=================================Putting Artifact On Nexus======================================"
        
        nexusArtifactUploader artifacts: [
            [
                artifactId: "${readPom.artifactId}",
                classifier: '',
                file: "target/${readPom.artifactId}-${readPom.version}.war",
                type: "${readPom.packaging}"
            ]
        
        ],
                
        credentialsId: 'nexus3', 
        groupId: "${readPom.groupId}", 
        nexusUrl: '172.31.8.152:8081', 
        nexusVersion: 'nexus3', 
        protocol: 'http', 
        repository: 'jenkins-nexus',
        version: "${readPom.version}"
        
        echo "==============================Artifact On Nexus Deployed Successfully=============================="
        
    }
    
}