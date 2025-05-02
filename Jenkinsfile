pipeline {
    agent any 
    options {
        timestamps()  // 타임스탬프 옵션 활성화
    }
    stages {
        stage('CheckOut') { 
            steps {
                echo "CheckOut" 
            }
        }
        stage('Build') { 
            steps {
                echo "Build" 
            }
        }
        stage('Deploy') { 
            steps {
                echo "Deploy"
            }
        }
    }
}
