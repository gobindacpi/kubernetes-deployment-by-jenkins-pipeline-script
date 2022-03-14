# kubernetes-deployment-by-jenkins-pipeline-script
~~~
First Install "kubernetes continuous Deploy" version 1.0.0 
~~~
(version 1.0.0. url:https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbHVwOVF2Um91VGxOa1FRWC1td29GRmZoYk5Rd3xBQ3Jtc0ttSUpSNV9SaDJpelhPSmZOaG9UODdiTk1RR25tVThwVDFFSWt1SDVDVkdoXzVEQmJpSTFiQ1gyd3d3UDhBeUNEZjRuSWpxMzBLV1dyTG43S1g0cms0VkQ4WV9ic21fdkFzaXdNRTFaNnlGdGZRWnhqVQ&q=https%3A%2F%2Fupdates.jenkins.io%2Fdownload%2Fplugins%2Fkubernetes-cd%2F1.0.0%2Fkubernetes-cd.hpi) 
~~~
(current version 2.3.1 will may not work) and assign kubernetes kubeconfig credential on jenkins credential file , then run below command on pipeline script.
~~~
~~~
pipeline {
  environment {
    registry = "gobindacpi/mywebsite"
    registryCredential = 'docker-hub'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git 'https://github.com/gobindacpi/mywebsite.git'
      }
    }
      stage('launch'){
          steps{
              script {
                  kubernetesDeploy(configs: "deployment.yaml", kubeconfigId: "KUBERNETES_CLUSTER_CONFIG")
              }
        }
    }
  }
}

~~~
