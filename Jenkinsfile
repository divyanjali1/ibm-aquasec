pipeline {
    agent {
        label 'divya'
    }
    stages {
        stage('Scan Base Image') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/divyanjali1/ibm-aquasec'
                sh label: '', script: 'trivy client --remote http://34.229.68.62:8080 centos:8'
            }
        }
        stage('Create Docker Image') {
            steps {
                sh label: '', script: 'docker build -t manngupta/devopsinaction:1.1 --build-arg downloadLink=http://apachemirror.wuchna.com/tomcat/tomcat-8/v8.5.57/bin/apache-tomcat-8.5.57.tar.gz --build-arg tomcatVersion=8.5.57 .'
            }
        }
        stage('Scan App Image') {
            steps {
                sh label: '', script: 'trivy client --remote http://34.229.68.62:8080 manngupta/devopsinaction:1.1'
            }
        }
    }
}
