pipeline {
    agent any
    tools {
        maven 'maven3'
        jdk 'java21'
    }
    stages{
        stage('Download Code from github'){
            steps{
                echo "Download Code from Github"
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/bheesham-devops/maven-jenkins10.git']])
            }      
        }
        stage('Run Build'){
            steps{
                echo "Run Build"
                sh 'mvn clean package'
            }      
        }
        stage('Archieve Artifacts'){
            steps{
                echo "Archive Artifacts"
                archiveArtifacts artifacts: '**/*.war', followSymlinks: false
            }      
        }
        stage('Trigger Deploy Job'){
            steps{
                echo "Trigger Deploy Job"
                build wait: false, job: 'deploypipeline'
            }      
        }
    }
}
