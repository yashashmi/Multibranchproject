node {
   def mvnHome
   stage('Preparation') { // for display purposes
      // Get some code from a GitHub repository
      git credentialsId: '88835265-1990-4e3e-8d78-f0832b3bdc0f', url: 'https://gitlab.com/vishnukiranreddy4/myproject.git'
      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured
      // **       in the global configuration.           
      mvnHome = tool 'MAVEN_HOME'
   }
   stage('CompileandPackage') {
      // Run the maven build
      withEnv(["MVN_HOME=$mvnHome"]) {
         if (isUnix()) {
            sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore clean package'
         } else {
            bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore clean package/)
         }
      }
   }
   stage('CodeAnalysis') {        
      withSonarQubeEnv {
         bat 'mvn sonar:sonar'
      }        
   }
   stage('DeploytoTomcat') {
      bat 'cp C:/JenkinsHomeDirectory/workspace/Multibranch-Pipeline_master/target/*.war C:/Tomcat8/webapps/'
   } 
   stage('FunctionalTesting') {
      sleep 60
	  bat label: '', script: 'mvn -Dfilename=testng-functional.xml surefire:test'
   }  
}
