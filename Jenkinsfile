node {
    stage('Configure') {
        env.PATH = "${tool 'M3'}/bin:${env.PATH}"
        version = '1.0.' + env.BUILD_NUMBER
        currentBuild.displayName = version

        properties([
                buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '', numToKeepStr: '10')),
                [$class: 'GithubProjectProperty', displayName: '', projectUrlStr: 'https://github.com/GauravEmani/spring-boot-sample/'],
                pipelineTriggers([[$class: 'GitHubPushTrigger']])
            ])
    }

    stage('Checkout') {
        git 'https://github.com/GauravEmani/spring-boot-sample/'
    }

    stage('Version') {
        
        "mvn -V"
    }

    stage('Build') {
       'mvn -B -V -U -e clean package'
    }

    stage('Archive') {
        junit allowEmptyResults: true, testResults: '**/target/**/TEST*.xml'
    }
	
	stage 'Gradle Static Analysis'
		withSonarQubeEnv {
			"mvn clean sonarqube"
		}
    
}