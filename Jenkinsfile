node {
    stage('SCM') {
        git 'https://github.com/Mao-xy/RiskManage.git'
    }
    stage('QA') {
        bat 'sonar-scanner'
    }
    stage('build') {
        def mvnHome = tool 'M3'
        bat "${mvnHome}\bin\mvn -B clean package"
    }
    stage('deploy') {
        bat "docker stop my || true"
        bat "docker rm my || true"
        bat "docker run --name my -p 11111:8080 -d tomcat"
        bat "docker cp target\RiskManage.war my:E:\tomcat\apache-tomcat-8.0.30\webapps"
    }
    stage('results') {
        archiveArtifacts artifacts: '**\target\*.war', fingerprint: true
    }
}
