pipeline {
   agent any

   tools {
       maven 'maven'
       jdk 'Java'
   }
  environment {
     dockerhub=credentials('dockerhub')
  }
   stages{
       stage("clean"){
      
         steps
            {
                sh 'mvn clean'
            }
       }

       stage("test"){
          when{
                branch "test"
                }
      
         steps
            {
                sh 'mvn test'
            }
       }

  stage('pack')
        {
            when{
                branch "prod"
                }
            steps{
                sh 'mvn package -DskipTests'
            }
        }
       stage('build image')
        {
            when{
                branch "prod"
                }
            steps{
                sh 'docker build -t capstone-img:1.01 .'
            }
        } 
        stage('pushing to dockerhub')
        {
            when{
                branch "prod"
                }
            steps{
                 sh 'docker tag capstone-img:1.01 yamikarajputd/capstone:1.01 '
                sh 'echo $dockerhub_PSW | docker login -u $dockerhub_USR --password-stdin'

                sh 'docker push yamikarajputd/capstone:1.01 '
            }


        }
      
      stage('DeployApp') {
      steps {
          
           
        kubernetesDeploy configs: '**/dep.yml', kubeConfig: [path: ''], kubeconfigId: 'kube', secretName: '', ssh: [sshCredentialsId: '*', sshServer: ''], textCredentials: [certificateAuthorityData: '', clientCertificateData: '', clientKeyData: '', serverUrl: 'https://']
             }
      
      
                
            }
   }
}


