pipeline {
  agent any
  tools {
    maven 'DHT_MVN'
    jdk 'DHT_SENSE'
  }
  stages {
    stage('check out') {
      steps {
        git(url: 'https://github.com/cs447-a6/maven-samples-A6', branch: 'master')
      }
    }

    stage('run') {
      steps {
        sh 'mvn clean test'
        catchError() {
          sh '''
                git bisect start 198644632661c67b6c32f59e9047c11a70685e15 98ac319c0cff47b4d39a1a7b61b4e195cfa231e5
                git bisect run mvn clean test
            '''
        }

      }
    }

  }
}