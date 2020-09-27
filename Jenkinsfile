pipeline {
  agent  any
  environment {
    GIT_COMMITTER_NAME = "Gopi Muruganantham"
    GIT_COMMITTER_EMAIL = "gopi.muruganantham@htcindia.com"
    classpath="D:\\IMPC0989_D\\Srping_Workspace\\MavenTest\\bin;D:\\IMPC0989_D\\.jar files\\selenium\\lib\\*"
    M2_HOME="D:\\apache-maven-3.3.9"
  }
  stages {
    stage("Preparing Code") {
      steps {
      checkout([$class: 'GitSCM', branches: [[name: '*/ThirdCommit']], 
						doGenerateSubmoduleConfigurations: false, 
						extensions: [], 
						submoduleCfg: [], 
						userRemoteConfigs: [[credentialsId: 'GH123', url: 'https://github.com/HTCTraining/MavenSpringMVC.git']]])
        
      }
    }
    
    stage("Build") {
      steps {
      
        bat '$M2_HOME\\bin\\mvn clean install -DskipTests'
      }
    }
    stage("Unit Testing") {
      steps {
      
        bat '$M2_HOME\\bin\\mvn test'
      }
    }
    stage("Unit Testing Result"){
      steps {
        archive "*/target/**/*"
        junit '*/target/surefire-reports/*.xml'
      }
    }
    
    stage('Automation Testing') {
       // Initiate Automation Testing
      steps{ 
        bat 'java org.testng.TestNG D:\\IMPC0989_D\\Srping_Workspace\\MavenTest\\bin\\testingspring.xml'
	}

   }
   stage('Deploy') {
       // Deploy the application
       steps{  
      bat 'copy C:\\Users\\gopim\\.jenkins\\workspace\\MavenSpringMVC\\target\\MavenSpringMVC.war D:\\eccat8.5\\webapps\\*'
   }
   }
    
  }
  post {
    
    success {
      mail(from: "bob@example.com", 
           to: "steve@example.com", 
           subject:"SUCCESS: ${currentBuild.fullDisplayName}",
           body: "Continuous Build & Deploy succeeded :-)")
    }

    failure {
      mail(from: "gopi.muruganantham@htcindia.com", 
           to: "gopi.muruganantham@htcindia.com", 
           subject: "FAILURE: ${currentBuild.fullDisplayName}", 
           body: "Automation failed :-(")
    }
    
  }
}			

				