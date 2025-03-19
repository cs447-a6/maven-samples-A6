pipeline {
  agent any
  stages {
    stage('check out') {
      steps {
        git(url: 'https://github.com/cs447-a6/maven-samples-A6', branch: 'master')
      }
    }

    stage('run') {
      steps {
        script {
          def status = sh(script: 'mvn clean test', returnStatus: true)
          if (status != 0) {
            currentBuild.result = 'UNSTABLE'
          }
        }
      }
    }

    stage('bisect') {
      when {
        expression { currentBuild.result == 'UNSTABLE' }
      }
      steps {
        sh 'git bisect start 198644632661c67b6c32f59e9047c11a70685e15 98ac319c0cff47b4d39a1a7b61b4e195cfa231e5'
        sh 'git bisect run mvn clean test'
      }
    }

  }
  tools {
    maven 'DHT_MVN'
    jdk 'DHT_SENSE'
  }
}
