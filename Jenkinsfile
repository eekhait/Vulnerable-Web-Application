pipeline { 
    agent any 
    stages { 
        stage ('Checkout') { 
            steps { 
                git branch:'master', url: 'https://github.com/eekhait/Vulnerable-Web-Application.git' 
            } 
        } 
        stage ('haha') { 
            steps { 
                sh "sonar-scanner.bat -D"sonar.projectKey=OWASP" -D"sonar.sources=." -D"sonar.host.url=http://localhost:9000" -D"sonar.login=b018a400139230be612732930fa0ee0cad8a1d99""
            } 
        } 
         
        stage('Code Quality Check via SonarQube') { 
           steps { 
               script { 
                def scannerHome = tool 'SonarQube'; 
                   withSonarQubeEnv('SonarQube') { 
                   sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=OWASP -Dsonar.sources=." 
                   } 
               } 
           } 
        } 
    } 
    post { 
        always { 
            recordIssues enabledForFailure: true, tool: sonarQube() 
        } 
    } 
} 
