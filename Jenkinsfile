node (label: 'slave1') {
stage('Build docker Images') {
			dir ('/tmp/workspace/devproject_pip') {
				sh 'sudo docker build -t httpd:staging-${BUILD_NUMBER} .'
				sh 'sudo docker tag httpd:staging-${BUILD_NUMBER} ganesh891/httpd:staging-${BUILD_NUMBER}'
				sh 'sudo docker login -u ganesh891 -p ganesh-1'
				sh 'sudo docker push ganesh891/httpd:staging-${BUILD_NUMBER}'	
				}
			}
stage('start Apache Service'){
				sh 'sudo docker run -p 80:80 -d --name container-${BUILD_NUMBER} ganesh891/httpd:staging-${BUILD_NUMBER}'
				}
stage('email notification'){
			emailext (
				subject: "Job '${env.JOB_NAME} ${env.BUILD_NUMBER}'",
				body: """<p>Check console output at <a href="${env.BUILD_URL}">${env.JOB_NAME}</a></p>""",
				to: "ganesan.kandasami@gmail.com",
				from: "ganesh@tcldevjenkins.com")
               }			
stage('clean workspace') {
		cleanWs()
}			
  }
