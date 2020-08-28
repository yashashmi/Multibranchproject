node {
   def mvnHome
   def scannerHome
   stage('Preparation') 
      git 'https://gitlab.com/vishnukiranreddy4/myproject.git'          
      mvnHome = tool 'MAVEN_HOME'
	  scannerHome = tool 'SonarScanner'
   }
    stage('CompileandPackage') {
        checkout scm
        sh 'mvn clean package -DskipTests'
    }    
    stage('CodeAnalysis') {
       withSonarQubeEnv("SonarCloud") {
                     sh "${tool("SonarScanner")}/bin/sonar-scanner"
        }
    }
    stage('DeploytoTomcat') {
        sh label: '', script: 'cp $(pwd)/target/*.war /opt/tomcat/webapps/'
    }    
}
