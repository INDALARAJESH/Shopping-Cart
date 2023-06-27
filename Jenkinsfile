pipeline{
    
    agent any 
    
    stages {
        
        stage('Git Checkout'){
            
            steps{
                
                script{
                    
                    git branch: 'main', url: 'https://github.com/INDALARAJESH/Shopping-Cart.git'
                }
            }
        }
        stage('UNIT testing'){
            
            steps{
                
                script{
                    
                    sh 'mvn test'
                }
            }
        }
        stage('Integration testing'){
            
            steps{
                
                script{
                    
                    sh 'mvn verify -DskipUnitTests'
                }
            }
        }
        stage('Maven build'){
            
            steps{
                
                script{
                    
                    sh 'mvn clean install'
                }
            }
        }
        stage('Static code analysis'){
            
            steps{
                
                script{
                    
                    withSonarQubeEnv(credentialsId: 'sonar-api') {
                        
                        sh 'mvn clean package sonar:sonar'
                    }
                   }
                    
                }
            }
            stage('Quality Gate Status'){
                
                steps{
                    
                    script{
                        
                        waitForQualityGate abortPipeline: false, credentialsId: 'sonar-api'
                    }
                }
            }
        }
        
}

// pipeline {
//     agent any
    // tools{
    //     jdk  'jdk11'
    //     maven  'maven3'
    // }
    
    // environment{
    //     SCANNER_HOME= tool 'sonar-scanner'
    // }
    
    // stages {
    //     stage('Git Checkout') {
    //         steps {
    //             git branch: 'main', url: 'https://github.com/INDALARAJESH/Shopping-Cart.git'
    //         }
    //     }
        
    //     stage('COMPILE') {
    //         steps {
    //             sh "mvn clean compile -DskipTests=true"
    //         }
    //     }
        
    //     stage('OWASP Scan') {
    //         steps {
    //             dependencyCheck additionalArguments: '--scan ./ ', odcInstallation: 'DP'
    //             dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
    //         }
        // }
        
        // stage('Sonarqube') {
        //     steps {
        //         withSonarQubeEnv('sonar-server'){
        //            sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=Shopping-Cart \
        //            -Dsonar.java.binaries=. \
        //            -Dsonar.projectKey=Shopping-Cart '''
        //        }
        //     }
        // }
        
        // stage('Build') {
        //     steps {
        //         sh "mvn clean package -DskipTests=true"
        //     }
        // }
        
        // stage('Docker Build & Push') {
        //     steps {
        //         script{
        //             withDockerRegistry(credentialsId: '2fe19d8a-3d12-4b82-ba20-9d22e6bf1672', toolName: 'docker') {
                        
        //                 sh "docker build -t shopping-cart -f docker/Dockerfile ."
        //                 sh "docker tag  shopping-cart adijaiswal/shopping-cart:latest"
        //                 sh "docker push adijaiswal/shopping-cart:latest"
        //             }
        //         }
        //     }
        // }
        
        
//     }
// }
