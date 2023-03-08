pipeline {
    
    agent any 
    
    stages {
        
        stage('SCM Checkout'){
           steps {
                git credentialsId: '1d874a1e-a28f-429e-b5bc-418685dca2dd', 
                url: 'https://github.com/Arjun3131/Jenkinsflow.git',
                branch: 'main'
           }
        }

        stage('Build'){
            steps{
                script{
                    sh '''
                    echo 'building with maven'
                    mvn clean install
                    '''
                }
            }
        }
        stage('Test') {
            steps {
                withsonarQubeEnv(){
                sh 'mvn sonar:sonar'
                }
            }
            post {
                always {
                    junit 'target/*.xml'
                }
            }
        }
      
          stage('Build Docker image and push'){
            steps{
               withCredentials([])
               sh docker build -t images:$BUILDNUM .
               sh docker push $BUILDimage:$BUILDNUM
        }
    }
}
