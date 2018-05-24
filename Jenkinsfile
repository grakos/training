node {
  stage('checkout') {
    git url:'https://github.com/spring-projects/spring-petclinic.git'
    //git url:'https://github.com/Accenture/spring-petclinic.git'
  }
  stage('build') {
    ansiColor('xterm') {
      def mvnHome = tool 'M3'
      sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore cobertura:cobertura -Dcobertura.report.format=xml clean package"
    }
  }
  
  stage('archive artifacts') {
      junit '**/target/surefire-reports/*.xml'
      archive 'target/spring-petclinic-*.jar'
  }
  
  stage('sonar') {
    ansiColor('xterm') {
      withSonarQubeEnv('SonarQubeServer') {
        def mvnHome = tool 'M3'
        sh "${mvnHome}/bin/mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.4.0.905:sonar"
      }
    }
  }
}

