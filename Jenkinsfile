pipeline {
   agent any
   tools {
       maven 'maven'
          jdk 'Java'
   }
  // environment {
    //  dockerhub=credentials('dockerhub')
 //  }
   stages{
       stage("clean"){
           
         steps
            {
                sh 'mvn clean'
            }
       }
       stage("test"){
           when {
        branch 'test'
            }
         steps
            {
                sh 'mvn clean test'
            }

   }
   stage("packaging"){
           
         steps
            {
                sh 'mvn package'
            }
       }
   }
}
