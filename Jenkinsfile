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
    stage('Artifact Job') {
      steps {
        build 'NexusBuild'
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

//Added by Jaya
def server = Artifactory.server('1234')
def downloadSpec = """{
 "files": [
  {
      "pattern": "MyNexusPipeline/*.zip",
      "target": "MyNexusPipeline/"
    }
 ]
}"""
server.download(downloadSpec)
def uploadSpec = """{
  "files": [
    {
      "pattern": "MyNexusPipeline/*.zip",
      "target": "MyNexusPipeline"
    }
 ]
}"""
server.upload(uploadSpec)
def buildInfo1 = server.download(downloadSpec)
def buildInfo2 = server.upload(uploadSpec)
buildInfo1.append(buildInfo2)
server.publishBuildInfo(buildInfo1)

def buildInfo = Artifactory.newBuildInfo()
server.download(artifactoryDownloadDsl, buildInfo)
server.upload(artifactoryUploadDsl, buildInfo)
server.publishBuildInfo(buildInfo)
