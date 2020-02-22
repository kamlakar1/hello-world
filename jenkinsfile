pipeline  {

          agent any  
          stages {
          stage (" SCM ") {
          steps {
          checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/kamlakar1/hello-world.git']]])
          }
         }
        
          stage (" COMPILE") {
          steps {
          sh 'mvn clean package'
        }
       }
    
         stage ("Archive Artifact") {
         steps {
         archiveArtifacts 'webapp/target/webapp.war' 
       }
      }
  
         stage (" EMAIL NOTIFICATION") {
         steps {
          
         mail bcc: '', body: '''Hiee,
         Build status''', cc: '', from: '', replyTo: '', subject: 'Build Status', to: 'kamlakarj4@gmail.com'
       }
      }
        stage (" Waiting for approval") {
        steps {
        input message: 'Waiting for approval', submitter: 'kamlakar', submitterParameter: 'kk'
      }
     }
    
       stage("Deploying on QA Server Through Ansible")  {
       steps {
       sshPublisher(publishers: [sshPublisherDesc(configName: 'Ansible-jenkins', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '/kk', remoteDirectorySDF: false, removePrefix: '', sourceFiles: 'webapp/target/*war'), sshTransfer(cleanRemote: false, excludes: '', execCommand: 'ansible-playbook play2.yml', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
     }
    }
  }
}



    
