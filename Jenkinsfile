node{

    stage("SCM Checkout"){
        
        echo "---------------------------- Pulling Application's code from Github--------------------------------"
        
        git url:'https://github.com/abhishekkishor/java-web-app-docker.git', branch: 'master'
        
        echo "---------------------------- Pulled Application's code--------------------------------"
        
    }
    stage("Maven Clean Package"){
        
        echo "-------------------------------Maven Process--------------------------------"
        
        sh "mvn clean package"
        
        echo "-------------------------------Now Archiving the Artifacts....------------------------------------"
        
        archiveArtifacts artifacts: '**/*.war'
        
        echo "-------------------------------Artifacts Archieved....------------------------------------"
        
        echo "-------------------------------Check Project's Status------------------------------------"
    }
    
}
