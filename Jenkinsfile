node('maven') {
  stage('Checkout') {
    git url: "https://github.com/agonzalezrh/nginx-ex", branch: "master"
  }
  stage('Test') {
    parallel(
      "Test Nginx": {
        sh "curl http://localhost"
      }
    )
  }
  stage('Build Image') {
    sh "oc start-build agonzalez --follow"
  }
  stage('Deploy') {
    openshiftDeploy depCfg: 'agonzalez'
    openshiftVerifyDeployment depCfg: 'agonzalez', replicaCount: 1, verifyReplicaCount: true
  }
  stage('System Test') {
    sh "curl -s -X GET http://agonzalez/"
  }
}
