pipeline {
    agent any

    stages {
        stage('Sonar Analysis') {
            steps {
                echo 'LMS Code Analysis'
                sh 'cd webapp && sudo docker run --rm -e SONAR_HOST_URL="http://54.81.4.56:9000" -v ".:/usr/src" -e SONAR_TOKEN="sqp_c2ee97e33b962332ccac96aab2f1645dc111e79f" sonarsource/sonar-scanner-cli -Dsonar.projectKey=lms'
            }
        }
        
        stage('Build LMS') {
            steps {
                echo 'LMS Build'
                sh 'cd webapp && npm install && npm run build'
            }
        }
        stage('Release LMS') {
            steps {
               script {  
                 echo 'Releasing...'
                 def packageJson = readJSON file: 'webapp/package.json'
                 def packageVersion = packageJSON.version
                 echo "${packageJSONVersion}"
                 sh "zip webapp/lms-${packageJSONVersion}.zip -r webapp/dist"
                 sh "curl -v -u admin:admin123 --upload-file webapp/lms-${packageJSONVersion}.zip http://54.81.4.56:8081/repository/lms/"
                }
            }

        }
        
    }
}

        
    
