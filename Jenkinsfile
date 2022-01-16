node
{
    def mavenHome = tool name: "Maven 3.8.4"
    
    stage('CheckoutCode')  
    {
        git branch: 'development', credentialsId: '9ede49a1-824d-4efd-aff5-ce7bda6d306f', url: 'https://github.com/sprithikaorg/maven-enterprise-application.git'
    }

    stage('Build') 
    {
        sh "${mavenHome}/bin/mvn clean package"
    }
    
    stage('sonarqubereport')
    {
      sh "${mavenHome}/bin/mvn clean sonar:sonar"  
    }
    
    stage('uploadartifact')
    {
        sh "${mavenHome}/bin/mvn clean deploy"
    }
    
    stage('Deployintotomcat')
    {
        sshagent(['be074315-ed3d-4455-8f33-b92e7f9eeb7f']) {
		sh "scp -o StrictHostKeyChecking=no target/maven-enterprise-application.war ec2-user@13.235.79.157:/opt/apache-tomcat-9.0.56/webapps"}
   
    }
    
}


