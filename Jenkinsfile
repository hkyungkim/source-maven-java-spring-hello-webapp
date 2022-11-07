pipeline {
  agent {
      label "jenkins-node"
    }

  triggers {
    //pollSCM('* * * * *')
    githubPush()
  }

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', 
        url: 'https://github.com/hkyungkim/source-maven-java-spring-hello-webapp.git'
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
        deploy adapters: [tomcat9(credentialsId: 'tomcat-manager', url: 'http://15.165.7.56:8080/')], contextPath: null, war: 'target/hello-world.war'
      }
    }
  }
}