pipeline {
  agent {
    label 'master'
  }
  stages {
    stage('Build') {
      steps {
        script {
          git 'https://github.com/ShakilaNatarajan/MavenNexusProject.git'
        }

        sh 'mvn clean install'
      }
    }
  }
  tools {
    maven 'Maven_Test'
  }
  environment {
    NEXUS_VERSION = 'nexus3'
    NEXUS_PROTOCOL = 'http'
    NEXUS_URL = '10.234.235.159:8081'
    NEXUS_REPOSITORY = 'Test'
    NEXUS_CREDENTIAL_ID = 'nexus-credentials'
  }
}