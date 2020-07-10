node {
    stage('CompileandPackage') {
        bat 'mvn clean package -DskipTests'
    }    
    stage('CodeAnalysis') {        
        withSonarQubeEnv {
            bat 'mvn sonar:sonar'
        }        
    }
    stage('DeploytoTomcat') {
        bat 'cp C:/JenkinsHomeDirectory/workspace/MyPipeline-Jenkinsfile/target/spring-project.war C:/Tomcat8/webapps/'
    }    
}