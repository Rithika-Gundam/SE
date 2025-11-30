/SE project
======Jenkins Pipeline Steps======
+New Item -> enter item name "pipeline-Navya"
under that-> click pipeline  -> ok
paste this code
pipeline {
    agent any

    tools {
        maven 'MAVEN_HOME'
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Cloning java-hello-world-with-maven repo'
                git branch: 'master', url: 'https://github.com/jabedhasan21/java-hello-world-with-maven.git'
            }
        }

        stage('Clean') {
            steps {
                echo 'Running mvn clean'
                bat "mvn clean"
            }
        }

        stage('Compile') {
            steps {
                echo 'Running mvn compile'
                bat "mvn compile"
            }
        }

        stage('Test') {
            steps {
                echo 'Running mvn test'
                bat "mvn test"
            }
        }

        stage('Package') {
            steps {
                echo 'Running mvn package'
                bat "mvn package"
            }
        }

        stage('Archive Artifact') {
            steps {
                echo 'Archiving JAR output'
                archiveArtifacts artifacts: "target/*.jar", fingerprint: true
            }
        }
    }

    post {
        success {
            echo '🎉 BUILD SUCCESS — JAR created and archived ✔'
        }
        failure {
            echo '❌ BUILD FAILED'
        }
    }
}    
click  Apply then save
click Build Now
click on green right symbol then click on pipeline overview  
DONE
