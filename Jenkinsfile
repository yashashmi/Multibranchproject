node {
    stage('CompileandPackage') {
        checkout scm
        sh 'mvn clean package -DskipTests'
    }    
    stage('CodeAnalysis') {
         steps {
            script {
               def scannerHome = tool 'SonarScanner';
                  withSonarQubeEnv("SonarCloud") {
                     sh "${tool("SonarScanner")}/bin/sonar-scanner"
                }
            }
        }
    }
    stage('DeploytoTomcat') {
        sh label: '', script: 'cp $(pwd)/target/*.war /opt/tomcat/webapps/'
    }    
}
