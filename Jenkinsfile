import groovy.json.JsonSlurper

def getFtpPublishProfile(def publishProfilesJson) {
  def pubProfiles = new JsonSlurper().parseText(publishProfilesJson)
  for (p in pubProfiles)
    if (p['publishMethod'] == 'FTP')
      return [url: p.publishUrl, username: p.userName, password: p.userPWD]
}

node {
  withEnv(['AZURE_SUBSCRIPTION_ID=9aab4416-7c5d-42e3-a1ce-018eb51fbe85',
        'AZURE_TENANT_ID=fa0a1ef4-7440-41db-8b65-92b20b3f344d']) {
    stage('init') {
      checkout scm
    }
  
    stage('build') {
      sh 'mvn clean package'
    }
  
//     stage('deploy') {
//       def resourceGroup = '<resource_group>'
//       def webAppName = '<app_name>'
//       // login Azure
//       withCredentials([usernamePassword(credentialsId: '<service_princial>', passwordVariable: 'AZURE_CLIENT_SECRET', usernameVariable: 'AZURE_CLIENT_ID')]) {
//        sh '''
//           az login --service-principal -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET -t $AZURE_TENANT_ID
//           az account set -s $AZURE_SUBSCRIPTION_ID
//         '''
//       }
//       // get publish settings
//       def pubProfilesJson = sh script: "az webapp deployment list-publishing-profiles -g $resourceGroup -n $webAppName", returnStdout: true
//       def ftpProfile = getFtpPublishProfile pubProfilesJson
//       // upload package
//       sh "curl -T target/calculator-1.0.war $ftpProfile.url/webapps/ROOT.war -u '$ftpProfile.username:$ftpProfile.password'"
//       // log out
//       sh 'az logout'
//     }
  }
}
