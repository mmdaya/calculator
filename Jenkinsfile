pipeline {
   agent any 

   tools {
      maven 'maven_tool'
   }

   stages {
      stage('BUILD') {
         steps {
               sh ''' 
                  cd calculator_app/
                  mvn clean package
               '''
         }
      }

      stage('UNIT TEST') {
         steps {
            dir("calculator_app/") {
               sh 'mvn clean test'
            }
         }
      }

      stage('Integration TEST') {
         steps {
            dir("calculator_app/") {
               sh 'mvn clean integration-test'
            }
         }
      }

      // stage('Deploy Tomcat Using maven plugin') {
      //    steps {
      //       dir("maven/calculator_app") {
      //          sh 'sudo mvn tomcat7:deploy'
      //       }
      //    }
      // }

      stage ('Deploy Tomcat Using jenkins plugin') {
         steps {
                script {
                    deploy adapters: [tomcat9(credentialsId: 'tomcat_manager', path: '', url: 'http://18.191.242.81:8081/')], 
                                     contextPath: '/calculator', 
                                     war: 'calculator_app/target/calculator.war'
                }
         }
      }
   }
}