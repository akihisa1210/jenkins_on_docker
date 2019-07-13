pipeline {
    agent any
    tools {
        maven "Maven 3.6.1"
        jdk "JDK 9.0.4"
    }
    stages {
        stage('Checkout') {
            steps {
                // Setting Git repository
                git url: 'https://github.com/akihisa1210/Jenkins_Practical_Guide_3rd_Edition.git'
            }
        }
        stage('Maven build') {
            steps {
                sh "mvn clean package"
            }
        }
        stage('Aggregate test results') {
            steps {
                // JUnit
                junit('target/surefire-reports/*.xml')
                // JaCoCo
                jacoco(execPattern: 'target/jacoco.exec')
            }
        }
        stage('Aggregate inspection results') {
            steps {
                // Checkstyle
                checkstyle(pattern: 'target/checkstyle-result.xml')
                // Findbugs
                findbugs(pattern: 'target/fundbugsXml.xml')
            }
        }
        stage('Trigger downstream job') {
            steps {
                build job: 'SamplePipeline_downstream',
                parameters: [string(name: 'MESSAGE', value: params.PERSON)]
            }
        }
        stage('Create 2 folders') {
            steps {
                parallel (
                    phase1: {
                        sh 'rm hoge'
                        sh 'mkdir hoge'
                    },
                    phase2: {
                        sh 'rm fuga'
                        sh 'mkdir fuga'
                    }
                )
            }
        }
    }
}
