pipeline{
  agent any 
  tools {
    maven "maven.3.8.6"
  }  
  stages {
    stage('1GetCode'){
      steps{
        sh "echo 'cloning the latest application version' "
        git branch: 'bug_fix', url: 'https://github.com/kyamranaliyev/multi-pipeline'
}
    }
    stage('2Test+Build'){
      steps{
        sh "echo 'running JUnit-test-cases' "
        sh "echo 'testing must passed to create artifacts ' "
        sh "mvn clean package"
      }
    }
    stage('3CodeQuality'){
      steps{
        sh "echo 'Perfoming CodeQualityAnalysis' "
        sh "mvn sonar:sonar"
      }
    } 
    stage('4uploadNexus'){
      steps{
        sh "mvn deploy"
      }
    }  
    stage('5deploy2prod'){
      steps{
      deploy adapters: [tomcat9(credentialsId: 'tomcat-abc-cred', path: '', url: 'http://52.91.90.162:8080/')], contextPath: null, war: 'target/*war'
}
}
}
}
