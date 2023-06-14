        pipeline{
            tools{
                jdk 'myjava'
                maven 'mymaven'
            }
            agent none
            stages{
                stage('Checkout on Master'){
                    agent any
                    steps{
                echo 'cloning...'
                        git 'https://github.com/theitern/DevOpsClassCode.git'
                    }
                }
                stage('Compile on Slave1'){
                    agent {label 'slave1'}
                    steps{
                        echo 'compiling...'
                        sh 'mvn compile'
                }
                }
                stage('CodeReview on Slave2'){
                    agent {label 'slave2'}
                    steps{
                    
                echo 'codeReview...'
                        sh 'mvn pmd:pmd'
                    }
                }
                stage('UnitTest on Slave3'){
                    agent {label 'slave3'}
                    steps{
                    echo 'Testing'
                        sh 'mvn test'
                    }
                    post {
                    success {
                        junit 'target/surefire-reports/*.xml'
                    }
                }	
                }
                stage('Package on Master'){
                    agent any
                    steps{
                        sh 'mvn package'
                    }
                }
            }
        }
