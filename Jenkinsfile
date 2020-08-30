pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'echo "Hello World"'
                sh '''
                    echo "Multiline shell steps works too"
                    ls -lah
                '''
            }
        }
       	stage('Lint HTML') {
	     steps {
	         sh 'tidy -q -e *.html'
	     }
	}
        stage('Upload to AWS') {
            steps {
                sh 'echo "Hello World" with AWS creds'
                withAWS(region:'us-west-2', credentials: 'aws-static') {
                    s3Upload(pathStyleAccessEnabled:true, payloadSigningEnabled:true, file:'index.html', bucket:'aws-static-jenkins-pipeline')
                }
            }
        }
    }
}
