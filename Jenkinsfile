pipeline {
  agent any
  stages {
    stage('git scm update') {
      steps {
        git url: 'https://github.com/dbdmfdms11/cicdtest.git', branch: 'main'
      }
    }
    stage('docker build and push') {
      steps {
        sh '''
        sudo docker build -t commit07/cicdtest:scm .
        sudo docker push commit07/cicdtest:scm
        '''
      }
    }
    stage('deploy kubernetes') {
      steps {
        sh '''
        ansible master -m command -a 'kubectl create deploy myweb3 --image=commit07/cicdtest:scm'
        ansible master -m command -a 'kubectl expose deploy myweb3 --type="LoadBalancer" --port=80 --target-port=80 --protocol="TCP"'
        ansible master -m command -a 'kubectl get svc'
        '''
      }
    }
  }
}
