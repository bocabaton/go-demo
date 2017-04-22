node('golang') {
	def root = tool name: 'Go 1.8.1', type: 'go'
	def version = '0.1.5'

	git([url: 'git@github.com:bocabaton/go-demo.git', branch: 'master', credentialsId: 'git-key'])

	stage('prep') {
		withEnv(["GOROOT=${root}", "GOPATH=${WORKSPACE}", "PATH+GO=${root}/bin"]) {
			sh 'go version'
		}
	}

	stage('build') {
		withEnv(["GOROOT=${root}", "GOPATH=${WORKSPACE}", "PATH+GO=${root}/bin"]) {
			sh 'cd $WORKSPACE && go build hello-world.go'
		}
	}

	stage('publish') {
		withEnv(["GOROOT=${root}", "GOPATH=${WORKSPACE}", "PATH+GO=${root}/bin"]) {
			sh 'cd $WORKSPACE && ./hello-world'
		}
	}
}