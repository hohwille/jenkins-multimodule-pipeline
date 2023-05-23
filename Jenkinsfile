pipeline {
  agent any
  tools {
    maven 'Maven 3.9.0'
    jdk 'jdk17'
    git 'Default'
  }
  stages {
    stage('Module1') {
      when { changeset "module1/**" }
      stages {
        stage('M1.Packaging') {
          steps {
            dir ('module1') {
              sh 'mvn  -B -ntp clean package'
              echo "Build is taking very long due to heavy work..."
              sh 'sleep 100000'
             }
          }
        }
        stage('M1.Installing') {
          when { changeset "module1/**" }
          steps {
            dir ('module1') {
              sh 'mvn  -B -ntp install'
            }
          }
        }
      }
    }
    stage('Module2') {
      when { changeset "module2/*" }
      stages {
        stage('M2.Packaging') {
          steps {
            dir ('module2') {
              sh 'mvn  -B -ntp clean package'
              echo "Build is taking very long due to heavy work..."
              sh 'sleep 100000'
            }
          }
        }
        stage('M2.Installing') {
          when { changeset "module1/*" }
          steps {
            dir ('module2') {
              sh 'mvn  -B -ntp install'
            }
          }
        }
      }
    }
  }
}