pipeline {

    agent {
        docker {
            image 'node'
            args '-u root'
        }
    }
    parameters {
        string(name: 'PARAM1', description: 'Param 1?')
        string(name: 'PARAM2', description: 'Param 2?')
    }
    stages {
        stage('Print') {
            steps {
                echo "Hello ${params.PARAM1}"
                echo "Hello ${params.PARAM2}"
            }
        }
        stage('Build') {
            steps {
                echo 'Building...'
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
                sh 'npm test'
            }
        }
        stage('Done') {
              steps {
                  echo 'I am done'
              }
          }
    }
    post {
        // Clean after build
        always {
            cleanWs(cleanWhenNotBuilt: false,
                    deleteDirs: true,
                    disableDeferredWipeout: true,
                    notFailBuild: true,
                    patterns: [[pattern: '.gitignore', type: 'INCLUDE'],
                               [pattern: '.propsfile', type: 'EXCLUDE']])
        }
    }
}
