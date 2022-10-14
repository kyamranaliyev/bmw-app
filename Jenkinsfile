pipeline {
    agent any
    tools{
    maven "maven.3.8.6"
    }
    stages{
        stage('1SCM'){
        steps{
            sh 'echo "bmw latest version"'
            git branch: 'bug_fix', url: 'https://github.com/kyamranaliyev/bmw-app'
        }
    }
    stage('2Test+Build'){
        steps{
            sh 'echo "running test cases"'
            sh "mvn clean install"
        }
    }
   stage('3CodeQuality'){
        steps{
            sh 'echo "performing code quality analysis"'
            sh "mvn sonar:sonar"
        }
   }
   stage('4Upload2Nexus'){
        steps{
            sh 'echo "uploading artifacts to artifactory"'
            sh "mvn deploy"
        }
   }
   stage('5Deploy2prod'){
        steps{
            sh 'echo "deploying to UAT"'
            deploy adapters: [tomcat9(credentialsId: 'tomcat-abc-cred', path: '', url: 'http://54.91.99.189:8080/')], contextPath: null, war: 'target/*war'
        }
   }
}
}
