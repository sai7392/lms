pipeline {
    agent any

    stages {
        stage('Sonar Analysis') {
            steps {
                echo 'LMS Code Analysis'
                sh 'cd webapp && sudo docker run --rm -e SONAR_HOST_URL="http://54.81.4.56:9000" -v ".:/usr/src" -e SONAR_TOKEN="sqp_c2ee97e33b962332ccac96aab2f1645dc111e79f" sonarsource/sonar-scanner-cli -Dsonar.projectKey=lms'
            }
        }
        
        
    }
}