node{
           def maven_home = tool name:"maven3.6.3"

    stage('git clone'){
        
        git branch: 'development', credentialsId: 'github_credential', url: 'https://github.com/chetandevopes/maven-web-application.git'
    }
    
      stage('create Buid'){
        
       sh "${maven_home}/bin/mvn clean package"
    }
    
     stage('sonarQube Report'){
        
       sh "${maven_home}/bin/mvn sonar:sonar "
       
    }
    
     stage('upload buid to nexus'){
        
       sh "${maven_home}/bin/mvn deploy "
    }
    
    stage('Deploy buid to Tomcat'){
        
        sshagent(['Tomcat_credential']) {

            sh "  scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.233.69.101:/opt/apache-tomcat-9.0.30/webapps/"
        }
       
    }
    
    
     stage('send email'){
        
      emailext body: ''' stage(\'upload buid to nexus\'){
        
       sh "${maven_home}/bin/mvn deploy "
    }''', subject: 'ffghjkl;werftgyhujikl;', to: 'panchalc468@gmail.com' 
       
    }

    
}
