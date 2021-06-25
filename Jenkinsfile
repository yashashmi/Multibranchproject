node {
   def mvnHome
   def scannerHome         
   mvnHome = tool 'MAVEN_HOME'
   scannerHome = tool 'SonarScanner'
   JavaHome = tool 'JAVA_HOME'
    stage('CompileandPackage') {
        git 'https://github.com/yashashmi/Multibranchproject.git'
        sh 'mvn clean package -DskipTests'
    }    
    stage('CodeAnalysis') {
        withEnv(["MVN_HOME=$mvnHome"]) {
       withSonarQubeEnv("SonarCloud") {
                     sh "${tool("SonarScanner")}/bin/sonar-scanner"
        }
        }
    }
    stage('DeploytoTomcat') {
        sh label: '', script: 'cp $(pwd)/target/*.war /opt/tomcat/webapps/'
    }    
}
