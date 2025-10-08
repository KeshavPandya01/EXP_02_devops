node {
    stage('Checkout') {
        checkout([$class: 'GitSCM',
                  branches: [[name: '*/main']],
                  userRemoteConfigs: [[url: 'https://github.com/keyurpatil06/jenkins-test.git']]
        ])
    }

    stage('Build') {
        withEnv(["JAVA_HOME=${tool 'jdk-21'}", "PATH+JAVA=${tool 'jdk-21'}/bin", "PATH+MAVEN=${tool 'maven'}/bin"]) {
            bat 'mvn clean package'
        }
    }

    stage('Test') {
        withEnv(["JAVA_HOME=${tool 'jdk-21'}", "PATH+JAVA=${tool 'jdk-21'}/bin", "PATH+MAVEN=${tool 'maven'}/bin"]) {
            bat 'mvn test'
        }
    }

    stage('Archive') {
        archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
    }
}
