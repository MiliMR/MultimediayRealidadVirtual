pipeline {
    agent any
    stages {
        stage('Compile') {
            steps {
                dir('dotty-example-project'){
                    sh 'pwd'
                    sh 'sbt clean compile'
                }
            }
        }
        stage('Dependencies Check') {
            steps {
                dir('dotty-example-project'){
                    sh 'pwd'
                    //sh 'sbt dependencyCheck'
                    //archiveArtifacts artifacts: '**/target/scala-0.24/*.html', fingerprint: true, onlyIfSuccessful: true
                    sh 'rm -rf build/owasp'
                    sh 'mkdir -p build/owasp'
                    dependencycheck additionalArguments: '--project dotty-example-project --scan . --out build/owasp/dependency-check-report.xml --format XML --noupdate', odcInstallation: 'Dependency Checker'
                    sh 'ls -alh build/owasp'
                    dependencyCheckPublisher pattern: 'build/owasp/dependency-check-report.xml'
                }
            }
        }
    }
}
