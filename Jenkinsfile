// define the secrets and the env variables
// engine version can be defined on secret, job, folder or global.
// the default is engine version 2 unless otherwise specified globally.
def secrets = [
  [path: 'secret/data/devops/jenkins/config', engineVersion: 2, secretValues: [
  [envVar: 'USERNAME', vaultKey: 'username'],
  [envVar: 'PASSWORD', vaultKey: 'password'] ]]
]

// optional configuration, if you do not provide this the next higher configuration
// (e.g. folder or global) will be used
def configuration = [vaultUrl: 'http://vault.hashi-vault.svc.cluster.local:8200',
                     vaultCredentialId: 'Vault-Jenkins-approle',
                      engineVersion: 2]
    

pipeline {
    agent {
        kubernetes {
            defaultContainer 'shell'
            yamlFile 'pod-template-sameCluster.yaml'
        }
    }
    
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
