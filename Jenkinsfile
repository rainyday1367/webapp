pipeline {
  agent any

  triggers {
    pollSCM('* * * * *')
  }

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', 
        url: 'https://github.com/rainyday1367/webapp'
      }
    }
    stage('Build') {
      steps {
        sh 'mvn clean package -DskipTests'
      }
    }
    stage('Test') {
      steps {
        sh 'mvn test'
      }
    }
    stage('Deploy') {
      steps {
           deploy adapters: [tomcat9(credentialsId: 'admin', url: 'http://192.168.56.102:8080')], 
           contextPath: 'hello-world', // 주소 끝에 붙는 경로 (/hello-world/)
           war: 'target/hello-world.war' // 빌드된 war 파일 위치
      }
    }
  }
}
