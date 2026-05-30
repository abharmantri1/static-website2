pipeline {
  agent any

  stages {

    stage('Checkout') {
      steps {
            echo 'Pulling Website code...'
            git branch: 'main', url: 'https://github.com/abharmantri1/static-website2.git'
      }
    }

    stage('Build Docker Image') {
      steps {
          powershell """
              docker build -t static-website:latest .
           """
      }
    }

    stage('Run Container') {
      steps {
        powershell """
             docker stop static-web 2>\$null
             docker rm static-web 2>\$null
             docker run -d --name static-web -p 5554:80 static-website:latest
             """
        }
      }
    }

  post {
      success {
           echo "website running at: http://localhost:5554"
          }
       }
  }
