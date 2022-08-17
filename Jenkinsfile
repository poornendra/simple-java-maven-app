pipeline {
    agent any

    stages {
        stage('Build') {
            steps {

                // Run Maven on a Unix agent.
                sh "mvn  clean install"
  
            }
        }
		stage('Deploy to Dev'){
		steps {
		sh 'mv target/*.war target/java.war'
		sshagent(['tomcatec2']) {
			//sh 'ssh ubuntu@172.31.40.143 rm -rf /opt/tomcat9/webapps/*.jar'
			//sh 'ssh ubuntu@18.143.91.234 sudo service tomcat restart'
		    sh 'scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/Java/target/java.war ec2-user@ipno:/usr/share/tomcat/webapps'
		    sh 'ssh -o StrictHostKeyChecking=no ec2-user@ipno sudo service tomcat restart'
		}
	}
	}
}
}
