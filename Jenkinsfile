pipeline {
   agent any 

   tools {
      maven 'maventool'
   }

   stages {
      stage('BUILD') {
         steps {
               sh '''
               mvn clean package
               '''
         }
      }

      stage('UNIT TEST') {
         steps {
            sh 'mvn clean test'
            sh 'mvn pmd:pmd'
         }
      }

      stage('Integration TEST') {
         steps {
            sh 'mvn clean integration-test'
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
                    deploy adapters: [tomcat9(credentialsId: 'tomcat_manager', path: '', 
                    url: 'http://3.137.42.112:8081/')], 
                    contextPath: '/calculator', 
                    war: 'target/calculator.war'
                }
         }
      }
   }
}
