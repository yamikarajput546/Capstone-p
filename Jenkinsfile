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
      
         steps
            {
                sh 'mvn test'
            }
       }
      

   stage("packaging"){
      when{
             branch 'prod'
          }
           
         steps
            {

                sh 'mvn package -DskipTests'

            

            }
       }
   }
}
