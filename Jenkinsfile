pipeline {
    agent any

    environment {
      GOPATH = "$HOME/go"
      PATH = "$PATH:$JENKINS_HOME/usr/local/go/bin:$GOPATH/bin"
    }

    stages {        
        stage('Go Install') {
            steps {
                echo 'Create go environment'
                sh 'mkdir -p $HOME/go/src'
                sh 'mkdir -p $HOME/go/bin'
                sh 'mkdir -p ${JENKINS_HOME}/usr/local'
                sh 'rm -rf $HOME/go/src/github/username/go_simple_rest/'
            }
        }

        stage('Go Test') {
            steps {
                echo 'Installing dependencies'
                sh 'go version'
                sh 'go get -u golang.org/x/lint/golint'
            }
        }

        stage('Git clone project') {
            steps {
                sh 'mkdir -p $HOME/go/src/github/username/go_simple_rest'
                sh 'git clone https://github.com/kt16a/go_simple_rest/ $HOME/go/src/github/username/go_simple_rest/'
            }
        }

        stage('Pre Test') {
            steps {
                dir("$HOME/go/src/github/username/go_simple_rest/") {
                    sh 'go build'
                }
            }
        }

        stage('Test') {
            steps {
                dir("$HOME/go/src/github/username/go_simple_rest/") {
                    echo 'Running vetting'
                    sh 'go vet .'
                    echo 'Running linting'
                    sh 'golint .'
                    echo 'Running test'
                    sh 'cd test && go test -v'
                }

            }
        }

    }
}
