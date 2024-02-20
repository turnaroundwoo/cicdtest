pipeline {
  agent any
  stages {
    stage('git scm update') {
      steps {
        git url: 'https://github.com/turnaroundwoo/cicdtest.git', branch: 'main'
      }
    }
    stage('docker build and push') {
      steps {
        sh '''
        sudo docker build -t seowooo3117/cicdtest:scm1 .
        sudo docker push seowooo3117/cicdtest:scm1
        '''
      }
    }
    stage('deploy kubernetes') {
      steps {
        sh '''
        ansible master -m command -a 'kubectl create deploy myweb4 --image=seowooo3117/cicdtest:blue'
        ansible master -m command -a 'kubectl expose deploy myweb4 --type="LoadBalancer" --port=80 --target-port=80 --protocol="TCP"'
        ansible master -m command -a 'kubectl get svc'
        '''
      }
    }
  }
}
