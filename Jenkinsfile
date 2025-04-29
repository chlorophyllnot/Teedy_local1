pipeline {
    agent any 
    tools {
        maven "Maven-3.9.9" // 确保这里使用的是你在 Jenkins 中配置的 Maven 名称
    }

    stages {
        stage('Clean') {
            steps {
                catchError(buildResult: 'SUCCESS', stageResult: 'ABORTED') {
                    sh 'mvn clean'
                }
            }
        }
        stage('Compile') {
            steps {
                catchError(buildResult: 'SUCCESS', stageResult: 'ABORTED') {
                    sh 'mvn compile'
                }
            }
        }
        stage('Test') {
            steps {
                catchError(buildResult: 'SUCCESS', stageResult: 'ABORTED') {
                    sh 'mvn test -Dmaven.test.failure.ignore=true'
                }
            }
        }
        stage('PMD') {
            steps {
                catchError(buildResult: 'SUCCESS', stageResult: 'ABORTED') {
                    sh 'mvn pmd:pmd'
                }
            }
        }
        stage('JaCoCo') {
            steps {
                catchError(buildResult: 'SUCCESS', stageResult: 'ABORTED') {
                    sh 'mvn jacoco:report'
                }
            }
        }
        stage('Javadoc') {
            steps {
                catchError(buildResult: 'SUCCESS', stageResult: 'ABORTED') {
                    sh 'mvn javadoc:javadoc'
                }
            }
        }
        stage('Site') {
            steps {
                catchError(buildResult: 'SUCCESS', stageResult: 'ABORTED') {
                    sh 'mvn site'
                }
            }
        }
        stage('Package') {
            steps {
                catchError(buildResult: 'SUCCESS', stageResult: 'ABORTED') {
                    sh 'mvn package -DskipTests'
                }
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/target/site/**/*.*', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true
            junit '**/target/surefire-reports/*.xml'
        }
    }
}
