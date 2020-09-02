node {
   def mvnHome
   def scannerHome         
   mvnHome = tool 'MAVEN_HOME'
   scannerHome = tool 'SonarScanner'
    stage('CompileandPackage') {
        git 'https://gitlab.com/vishnukiranreddy4/Multibranchproject.git'
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