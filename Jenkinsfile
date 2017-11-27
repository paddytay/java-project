properties([pipelineTriggers([githubPush()])])

node('linux') {   
	stage('Unit Tests') {    
		git 'https://github.com/paddytay/java-project.git'
		sh 'ant -f test.xml -v'
		junit 'reports/result.xml'
	}   
	stage('Build') {    
		sh 'ant -f build.xml -v'
	}   
	stage('Deploy') {
	    withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: '75abdb7b-88d2-422b-9fbf-35da72c50bb4', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
    sh 'aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins'
}
	}
	stage('Report') {
		junit 'reports/result.xml'   
	}
}
