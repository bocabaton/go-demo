node('golang') {
	def root = tool name: 'Go 1.9', type: 'go'
	def version = '0.1.0'

	git([url: 'git@github.com:bocabaton/go-demo.git', branch: 'master', credentialsId: 'git-key'])

	stage('prep') {
		withEnv(["GOROOT=${root}", "GOPATH=${WORKSPACE}", "PATH+GO=${root}/bin"]) {
			sh 'go version'
		}
	}

	stage('test') {
		withEnv(["GOROOT=${root}", "GOPATH=${WORKSPACE}", "PATH+GO=${root}/bin"]) {
			sh 'cd $WORKSPACE && go run go-demo.go'
		}
	}

	stage('build') {
		withEnv(["GOROOT=${root}", "GOPATH=${WORKSPACE}", "PATH+GO=${root}/bin"]) {
			sh 'cd $WORKSPACE && go build go-demo.go'
		}
	}

	stage('package') {
		withEnv(["GOROOT=${root}", "GOPATH=${WORKSPACE}", "PATH+GO=${root}/bin"]) {
			sh 'cd $WORKSPACE && tar -cvzf go-demo.tar.gz go-demo.go'
		}
	}

	stage('publish') {
		nexusArtifactUploader artifacts: [[ artifactId: 'go-demo',
											classifier: '',
											file: 'go-demo.tar.gz',
											type: 'bin' ]],
							  credentialsId: 'nexus-deploy',
							  groupId: 'com.github.bocabaton.go-demo',
							  nexusUrl: 'nexus',
							  nexusVersion: 'nexus3',
							  protocol: 'https',
							  repository: 'maven-releases',
							  version: version
	}
}