def COLOR_MAP = [
    'SUCCESS':'good',
    'FAILURE':'danger'
]

pipeline {
    agent any

    // these tools are saved in global tool configuration
    tools {
        maven "MAVEN3"
        jdk "OracleJDK8"
    }

    // environment {
    //     SNAP_REPO = 'vprofile-snapshot'
    //     NEXUS_USER = 'admin'
    //     NEXUS_PASS = 'admin_vp'
    //     RELEASE_REPO = 'vprofile-release'
    //     CENTRAL_REPO = 'vpro-maven-central'
    //     NEXUSIP = '172.31.18.106'
    //     NEXUSPORT = '8081'
    //     NEXUS_GRP_REPO = 'vpro-maven-group'
    //     NEXUS_LOGIN = 'nexuslogin'
    //     SONARSERVER = 'sonarserver'
    //     SONARSCANNER = 'sonarscanner' 
    // }

    environment {

        CI = true
        ARTIFACTORY_ACCESS_TOKEN = credentials('jfrogtoken')
        JFROG_PASSWORD = credentials('jfrog-password')
    }

    stages {
        stage ('Checkout Git Repository') {
            steps {
                git branch: 'artifactory', url: 'https://github.com/JohnLawliet/vprofile-project.git'
            }
        }
        stage ('Build maven job') {
            steps {
                sh './mvn install'
            }
        }
    }

    

    // stages {
    //     // stage('FETCH CODE') {
    //     //     steps {
    //     //         git branch: 'vp-rem', url: 'https://github.com/JohnLawliet/vprofile-project.git'
    //     //     }
    //     // }


    //     stage('Build'){
    //         steps {
    //             sh 'mvn -s settings.xml -DskipTests install'
    //         }
    //         // if success, archive all wars
    //         post {
    //             success {
    //                 echo "Now archiving..."
    //                 archiveArtifacts artifacts: '**/*.war'
    //             }
    //         }
    //     }

    //     // tests run by maven
    //     // NOTE: add -s settings wherever there is mvn command to ensure maven takes in from nexus repositories
    //     stage('TEST') {
    //         steps {
    //             sh 'mvn -s settings.xml test'
    //         }
    //     }

    //     // this checks source code quality like what all can be improved in the code
    //     stage ('Checkstyle Analysis') {
    //         steps {
    //             sh 'mvn -s settings.xml checkstyle:checkstyle'
    //         }
    //     }

    //     stage ('Sonar Analysis') {
    //         environment {
    //             scannerHome = tool "${SONARSCANNER}"
    //         }
    //         steps {
    //             //fields provided with -Dsonar are parameters that can be passed to sonarqube scanner. Find ind docs
    //             //the reports can be found in the workspace of each successful deployment within target directory created after successful deployment. Note that files like surefire-report, jacoco, checkstyle are received from above test stages
    //             withSonarQubeEnv ("${SONARSERVER}") {
    //                 sh '''${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=vprofile \
    //                 -Dsonar.projectName=vprofile \
    //                 -Dsonar.projectVersion=1.0 \
    //                 -Dsonar.sources=src/ \
    //                 -Dsonar.java.binaries=target/test-classes/com/visualpathit/account \
    //                 -Dsonar.junit.reportsPath=target/surefire-reports/ \
    //                 -Dsonar.jacoco.reportsPath=target/jacoco.exec \
    //                 -Dsonar.java.checkstyle.reportPaths=target/checkstyle-result.xml
    //                 '''
    //             }
    //         }
    //     }

    //     stage ('Quality Gate') {
    //         steps {
    //             timeout(time: 1, unit: 'HOURS') {
    //                 waitForQualityGate abortPipeline: true
    //             }
    //         }
    //     }

    //     //Note: the steps content here is copy pasted from github docs for jenkins plugin nexusArtifactuploader plugin
    //     //jenkins has built in variables like BUILD_ID, BUILD_TIMESTAMP which needs to be accessed via env.<var name>. Build ID is the nth number of time, the source code got deployed
    //     stage ('Upload Artifact') {
    //         steps {
    //             nexusArtifactUploader(
    //                 nexusVersion: 'nexus3',
    //                 protocol: 'http',
    //                 nexusUrl: "${NEXUSIP}:${NEXUSPORT}",
    //                 groupId: 'QA',
    //                 version: "${env.BUILD_ID}-${env.BUILD_TIMESTAMP}",
    //                 repository: "${RELEASE_REPO}",
    //                 credentialsId: "${NEXUS_LOGIN}",
    //                 artifacts: [
    //                     [artifactId: 'vproapp',
    //                     classifier: '',
    //                     file: 'target/vprofile-v2.war',
    //                     type: 'war']
    //                 ]
    //             )
    //         }
    //     }
    // }

    // post {
    //     always {
    //         echo 'Slack Notifications.'
    //         slackSend channel: '#devops',
    //             color: COLOR_MAP[currentBuild.currentResult],
    //             message: "*${currentBuild.currentResult}:* Job ${env.JOB_NAME} build ${env.BUILD_NUMBER} \n More info at: ${env.BUILD_URL}"
    //     }
    // }
} 