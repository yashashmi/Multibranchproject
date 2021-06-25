node {
   def mvnHome
   def scannerHome
   stage('Preparation') { // for display purposes
      // Get some code from a GitHub repository
      git 'https://github.com/yashashmi/Multibranchproject.git'
      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured
      // **       in the global configuration.           
      mvnHome = tool 'MAVEN_HOME'
	  scannerHome = tool 'SonarScanner'
	  JavaHome = tool 'JAVA_HOME'
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
	   withEnv(["JAVA_HOME=$JavaHome"]) {
      withSonarQubeEnv("SonarCloud") {
                     sh "${tool("SonarScanner")}/bin/sonar-scanner"
                  }
            }
   }
   stage('DeploytoTomcat') {
      sh 'cp $(pwd)/target/*.war /opt/tomcat/webapps/'
   } 
   stage('FunctionalTesting') {
      sleep 60
	  sh label: '', script: 'mvn -Dfilename=testng-functional.xml surefire:test'
   }  
}
