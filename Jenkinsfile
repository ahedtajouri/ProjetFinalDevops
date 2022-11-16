pipeline
{
    agent any 
    
   
    stages{
        stage('cloner projet'){
            steps {
               git branch: 'main', url: 'https://github.com/ahedtajouri/ProjetFinalDevops.git'
            }
        }
        
         stage('install'){
            steps {
               sh 'mvn install'
            }
        }
        stage('Clean'){
            steps {
               sh 'mvn clean'
            }
            
        }
        
         stage('Clean Package'){
            steps {
               sh 'mvn clean package'
            }
            
        }
        
        stage('Compilation'){
            steps {
               sh 'mvn compile'
            }
            
        }
       stage('MOCKITO') {
            steps {
          sh 'mvn clean test -Dtest=com.esprit.examen.services.ProduitServiceTest'
            }
        }
            
           stage('SonarQube analysis') {
            steps {
                sh 'mvn clean package sonar:sonar -Dsonar.login=admin -Dsonar.password=adminadmin'
            }
           }
           
            stage('Nexus') {
            steps {
                sh 'mvn deploy -Dnexus.login=admin -Dnexus.password=adminadmin'
            }
           }
           
           
        stage("Building Docker Image") {
                steps{
                   // sh 'sudo chmod 666 /var/run/docker.sock'
                    sh 'docker build -t khalil999/produit1 .'
                }
        }
        
       stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u khalil999 --password adminadmin'
			}
		}

		stage('Push') {

			steps {
				sh 'docker  push khalil999/produit1:latest'
			}
		} 
		stage('Start container') {
             steps {
               
                sh 'docker-compose up -d --force-recreate --build'
                
      }
        }
        
   
   }
        
    }