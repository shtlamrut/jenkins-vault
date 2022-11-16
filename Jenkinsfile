// define the secrets and the env variables
// engine version can be defined on secret, job, folder or global.
// the default is engine version 2 unless otherwise specified globally.
def secrets = [
  [path: 'secret/data/devops/jenkins/config', engineVersion: 1, secretValues: [
  [envVar: 'USERNAME', vaultKey: 'username'],
  [envVar: 'PASSWORD', vaultKey: 'password'] ]]
]

// optional configuration, if you do not provide this the next higher configuration
// (e.g. folder or global) will be used
def configuration = [vaultUrl: 'http://vault.default.svc.cluster.local:8200',
                     vaultCredentialId: 'jenkins-vault',
                      engineVersion: 2]
    

pipeline {
    agent any
    
    stages {
        
        stage('Vault') {
            steps {
                withVault([configuration: configuration, vaultSecrets: secrets]) {
                  sh "echo ${env.USERNAME}"
                  sh "echo ${env.PASSWORD}"
                  
                }
            }  
        }
    }    
}

