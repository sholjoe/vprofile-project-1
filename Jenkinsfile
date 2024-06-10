pipeline {
    agent any
    tools {
        maven "MAVEN3"
        jdk "OracleJDK8"
    }

    environment {
        SNAP_REPO = 'vprofile-snapshot'
        NEXUS_USER = 'admin'
        NEXUS_PASS = 'admin123'
        RELEASE_REPO = 'vprofile-release'
        CENTRAL_REPO = 'vpro-maven-central'
        NEXUSIP = '172.31.54.108'
        NEXUSPORT = '8081'
        NEXUS_GRP_REPO = 'vpro-maven-group'
        NEXUS_LOGIN = 'nexuslogin'
    }

    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }
        
        stage('Build') {
            steps {
                // Ensure the environment variables are printed for debugging
                sh 'echo NEXUSIP=$NEXUSIP'
                sh 'echo NEXUSPORT=$NEXUSPORT'
                sh 'echo NEXUS_USER=$NEXUS_USER'
                sh 'echo NEXUS_PASS=$NEXUS_PASS'
                sh 'echo SNAP_REPO=$SNAP_REPO'
                sh 'echo RELEASE_REPO=$RELEASE_REPO'
                sh 'echo CENTRAL_REPO=$CENTRAL_REPO'
                sh 'echo NEXUS_GRP_REPO=$NEXUS_GRP_REPO'

                // Run the Maven build
                sh 'mvn clean install -DskipTests -s settings.xml'
            }
        }
    }

    post {
        always {
            echo 'Pipeline has completed.'
        }
        success {
            echo 'Build completed successfully.'
        }
        failure {
            echo 'Build failed.'
        }
    }
}


