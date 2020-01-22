pipeline {
  agent none
  stages {
    stage('compile') {
      steps {
        build '10_Integration'
      }
    }

    stage('static code analyse') {
      parallel {
        stage('static code analyse') {
          steps {
            build '20-Static-Code-Analyze\\Check-10_Integration'
          }
        }

        stage('dynamic code analyse') {
          steps {
            build '30-Dynamic-Code-Analyze\\Check-10_Integrarion'
          }
        }

        stage('SW-FITs') {
          steps {
            build '30-Dynamic-Code-Analyze\\83%	SW-FITS-10_Integration'
          }
        }

      }
    }

    stage('collect results') {
      steps {
        copyArtifacts '20-Static-Code-Analyze\\10_Integration'
        junit(testResults: '*.junit.xml', allowEmptyResults: true)
      }
    }

  }
}