pipeline {
  agent any
  
  stages { 
    stage('Lint HTML') {
            steps {
                  sh 'tidy -q -e *.html'
                  }
                       }
    stage('Upload to AWS') {
              steps {
                  withAWS(region:'us-west-2',credentials:'aws-static') {
                  sh 'echo "Uploading content with AWS creds"'
                      s3Upload(pathStyleAccessEnabled:true, payloadSigningEnabled: true, file:'index.html', bucket:'devopsjenkins')
                  }
              }
         }

    stage('curl Test') {
            steps {
              sh 'echo "Testing... should return HTTP/1.1 200 OK"'
              sh ''' 
              curl -I http://devopsjenkins.s3-website-us-west-2.amazonaws.com/
              curl http://devopsjenkins.s3-website-us-west-2.amazonaws.com/
                
              '''  
                }
    }
  }

}
