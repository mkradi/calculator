pipeline {
     agent any
     triggers {
        pollSCM('* * * * *')
    }
     stages {
          stage("Compile") {
               steps {
                    sh "./gradlew compileJava"
               }
          }
          stage("Unit test") {
               steps {
                    sh "./gradlew test"
               }
          }
          
        stage("Static code analysis") {
            steps {
                sh "./gradlew checkstyleMain"
            }
        }

        stage("Package") {
            steps {
                sh "./gradlew build"
            }
        }

        stage("Docker build") {
            steps {
                sh "docker build -t oahudock99/calculator ."
            }
        }
        stage("Docker push") {
            steps {
                sh "docker push oahudock99/calculator"
            }
        }
        stage("Deploy to staging") {
            steps {
                sh "docker run -d --rm -p 8765:8080 --name calculator oahudock99/calculator"
            }
        }
     }
}