node {
  stage('build & deploy') {
    openshiftBuild bldCfg: ‘angular-web-app’,
      namespace: 'development',
      showBuildLogs: 'true'
    openshiftVerifyDeployment depCfg: 'angular-web-app',
      namespace: 'development'
  }
  stage('approval (test)') {
    input message: 'Approve for testing?',
      id: 'approval'
  }
  stage('deploy to test') {
    openshiftTag srcStream: 'angular-web-app',
      namespace: 'development',
      srcTag: 'latest',
      destinationNamespace: 'testing',
      destStream: 'angular-web-app',
      destTag: 'test'
    openshiftVerifyDeployment depCfg: 'angular-web-app',
      namespace: 'testing'
  }
  stage('approval (production)') {
    input message: 'Approve for production?',
      id: 'approval'
  }
  stage('deploy to production') {
    openshiftTag srcStream: 'angular-web-app',
      namespace: 'development',
      srcTag: 'latest',
      destinationNamespace: 'production',
      destStream: 'angular-web-app',
      destTag: 'prod'
    openshiftVerifyDeployment depCfg: 'angular-web-app',
      namespace: 'production'
  }
}
