pipeline{
  agent any 
  tools {
    maven "maven.3.8.6"
  }  
  stages {
    stage('1GetCode'){
      steps{
        sh "echo 'cloning the latest application version' "
git credentialsId: 'githubcred', url: 'https://github.com/kyamranaliyev/maven-web-application'   
}
    }
    stage('3Test+Build'){
      steps{
        sh "echo 'running JUnit-test-cases' "
        sh "echo 'testing must passed to create artifacts ' "
        sh "mvn clean package"
      }
    }
    stage('4CodeQuality'){
      steps{
        sh "echo 'Perfoming CodeQualityAnalysis' "
        sh "mvn sonar:sonar"
      }
    } 
    stage('5uploadNexus'){
      steps{
        sh "mvn deploy"
      }
    }  
    stage('8deploy2prod'){
      steps{
deploy adapters: [tomcat9(credentialsId: 'tomcat-abc-cred', path: '', url: 'http://54.164.71.145:8080')], contextPath: null, war: 'target/*war'
}
}
}
}
