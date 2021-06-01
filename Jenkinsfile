node('master') 
  {
      stage('gitcheckout') 
     {
          git 'https://github.com/wakaleo/game-of-life.git'
     }
      stage('mavenbuild')
     {
        withMaven(maven: 'maven') 
        {
         sh "mvn clean install"
        }
     }    
      stage('nexusartifactsuploader')
     {
          nexusArtifactUploader artifacts: [[artifactId: 'dev', classifier: '', file: 'gameoflife-web/target/gameoflife.war', type: 'war']], credentialsId: '123', groupId: 'dev', nexusUrl: '18.220.141.111:8081/nexus', nexusVersion: 'nexus2', protocol: 'http', repository: 'dev', version: '$BUILD_ID'
     }
      stage('deploy war/ear to container')
      {
          deploy adapters: [tomcat8(credentialsId: 'tomcat123', path: '', url: 'http://18.220.141.111:8080')], contextPath: null, war: 'gameoflife-web/target/gameoflife.war'
      }
      stage('message')
      {
          echo "pipeline is done"
      }
  }
