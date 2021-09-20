pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Build demo-app'
        sh 'sh run_build_script.sh'
      }
    }

    stage('Linux Test') {
      parallel {
        stage('Linux Test') {
          steps {
            echo 'Run Linux Test'
            sh 'sh run_linux_test.sh'
          }
        }

        stage('Windows Test') {
          steps {
            echo 'Run Windows Test'
          }
        }

      }
    }

    stage('Deploy Staging') {
      steps {
        echo 'Deploy to staging enviroment'
      }
    }

    stage('Deploy Production') {
      steps {
        echo 'Deploy to production enviroment'
      }
    }

  }
  post {
    always {
      archiveArtifacts(artifacts: 'target/demoapp.jar', fingerprint: true)
    }

    failure {
      mail(to: 'ci-team@example.com', subject: "Failed Pipiline ${currentBuild.fullDisplayName}", body: "For details about the feilure, see ${env.BIULD_URL}")
    }

  }
}