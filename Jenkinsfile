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

   stage("packaging"){
      when{
             branch 'prod'
          }
           
         steps
            {

                sh 'mvn package -DskipTests'

            

            }
       }
      stage('deploy')
         {
//             when{
//                 branch "prod"
//                  }
            steps{
                script{
                   kubernetesDeploy configs: '**/sts.yaml', kubeConfig: [path: ''], kubeconfigId: 'kubeconfig', secretName: '', ssh: [sshCredentialsId: '*', sshServer: ''], textCredentials: [certificateAuthorityData: '', clientCertificateData: '', clientKeyData: '', serverUrl: 'https://']
                }
            }
      
      
      
      
      
      
   }
}
