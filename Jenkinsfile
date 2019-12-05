pipeline {
    agent {
        docker {
            image 'maven:3-alpine' 
            args '-v /var/maven_home/m2:/root/.m2' 
        }
    }
    stages {
        stage('Build') { 
            steps {
                sh 'mvn -B -DskipTests -DproxySet=true -DproxyHost=marc.proxy.corp.sopra -DproxyPort=8080 Dhttp.nonProxyHosts=localhost|127.0.0.1 clean package' 
            }
        }
		
        stage('Test') { 
            steps {
				withSonarQubeEnv('SonarScanner') {			
                sh 'mvn -B -e -DskipTests -DproxySet=true -DproxyHost=marc.proxy.corp.sopra -DproxyPort=8080 Dhttp.nonProxyHosts=localhost|127.0.0.1 verify sonar:sonar' 
				}
            }
        }		
    }
}
