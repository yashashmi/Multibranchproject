node {
    stage('CompileandPackage') {
        checkout scm
        bat 'mvn clean package -DskipTests'
    }    
    stage('CodeAnalysis') {        
        withSonarQubeEnv {
            bat 'mvn sonar:sonar'
        }        
    }
    stage('DeploytoTomcat') {
        bat 'cp C:/JenkinsHomeDirectory/workspace/Multibranch-Pipeline_develop/target/spring-project.war C:/Tomcat8/webapps/'
    }    
}
