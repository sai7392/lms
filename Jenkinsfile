pipeline {
    agent any

    stages {
        stage('Sonar Analysis') {
            steps {
                echo 'LMS Code Analysis'
                sh 'cd webapp && sudo docker run --rm -e SONAR_HOST_URL="http://52.56.245.199:9000" -v ".:/usr/src" -e SONAR_TOKEN="sqp_fe1fd3c6e2f569ee40e70560618bf9483ea4bc9c" sonarsource/sonar-scanner-cli -Dsonar.projectKey=lms'
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
                    echo "Publish LMS Artifacts"       
                    def packageJSON = readJSON file: 'webapp/package.json'
                    def packageJSONVersion = packageJSON.version
                    echo "${packageJSONVersion}"  
                    sh "zip webapp/dist-${packageJSONVersion}.zip -r webapp/dist"
                    sh "curl -v -u admin:admin123 --upload-file webapp/dist-${packageJSONVersion}.zip http://52.56.245.199:8081/repository/lms/"     
            }
            }
        }
	
	        stage('Deploy LMS') {
            steps {
                script {
                    echo "Deploy LMS"       
                    def packageJSON = readJSON file: 'webapp/package.json'
                    def packageJSONVersion = packageJSON.version
                    echo "${packageJSONVersion}"  
                    sh "curl -u admin:admin123 -X GET \'http://52.56.245.199:8081/repository/lms/dist-${packageJSONVersion}.zip\' --output dist-'${packageJSONVersion}'.zip"
                    sh 'sudo rm -rf /var/www/html/*'
                    sh "sudo unzip -o dist-'${packageJSONVersion}'.zip"
                    sh "sudo cp -r webapp/dist/* /var/www/html"
            }
            }
        }
    }

        
  }


        
    
