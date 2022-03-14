# kubernetes-deployment-by-jenkins-pipeline-script
~~~
First Install "kubernetes continuous Deploy" version 1.0.0 
~~~
(version 1.0.0. urlhttps://mirrors.tuna.tsinghua.edu.cn/jenkins/plugins/kubernetes-cd/1.0.0/kubernetes-cd.hpi) 
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
