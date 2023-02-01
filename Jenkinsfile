pipeline {
    agent any

    // these tools are saved in global tool configuration
    tools {
        maven "MAVEN3"
        jdk "OracleJDK8"
    }

    environment {
        SNAPREPO = 'vprofile-snapshot'
        NEXUSUSER = 'admin'
        NEXUSPASS = 'admin_vp'
        RELEASEREPO = 'vprofile-release'
        CENTRALREPO = 'vpro-maven-central'
        NEXUSIP = '172.31.18.106'
        NEXUSPORT = '8081'
        NEXUSGRPREPO = 'vpro-maven-group'
        NEXUSLOGIN = 'nexuslogin'
    }

    stages {
        stage('Build'){
            steps {
                sh 'mvn -s settings.xml -DskipTests install'
            }
        }
    }
}