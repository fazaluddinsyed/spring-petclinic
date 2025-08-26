pipeline {
  agent any
  tools { jdk 'jdk17'; maven 'maven3' }
  options { timestamps(); skipDefaultCheckout(true) }

  stages {
    stage('Checkout') {
      steps {
        checkout([$class: 'GitSCM',
          branches: [[name: '*/main']],
          userRemoteConfigs: [[url: 'https://github.com/<your-username>/spring-petclinic.git']]
        ])
      }
    }
    stage('Build')     { steps { sh 'mvn -B -DskipTests clean package' } }
    stage('Test')      { steps { sh 'mvn -B test' }
                         post { always { junit 'target/surefire-reports/*.xml' } } }
    stage('Archive')   { steps { archiveArtifacts artifacts: 'target/*.jar', fingerprint: true } }
  }
}
