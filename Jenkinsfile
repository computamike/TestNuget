pipeline {
  agent {
    docker {
      image 'apcovernight/continuous-integration:latest'
      args '''-u root
-v /var/run/docker.sock:/var/run/docker.sock'''
    }

  }
  stages {
    stage('Print Message') {
      steps {
        echo 'Starting Processing'
        sh '/usr/share/dotnet/dotnet -h'
      }
    }

    stage('.Net Restore') {
      steps {
        dir(path: "${env.WORKSPACE}") {
          sh 'pwd'
          sh 'whoami'
          sh 'dotnet restore'
        }

      }
    }

    stage('.Net Publish') {
      steps {
        dir(path: "${env.WORKSPACE}") {
          sh 'pwd'
          sh 'dotnet publish -c release'
        }

      }
    }

    stage('.Net Test') {
      steps {
        dir(path: "${env.WORKSPACE}") {
          sh 'pwd'
          sh 'dotnet test'
        }

      }
    }

  }
  post {
    always {
      sh 'chmod -R 777 .'
      cleanWs()
    }

  }
}