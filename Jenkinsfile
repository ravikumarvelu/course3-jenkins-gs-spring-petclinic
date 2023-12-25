pipeline{
    agent any
    stages{
        stage("checkout"){
            steps{
                git branch: 'main', url: 'https://github.com/ravikumarvelu/course3-jenkins-gs-spring-petclinic.git'
            }
            
        }
        stage("build"){
            steps{
                bat "./mvnw package"
            }
            
        }
        stage("capture"){
            steps{
                archiveArtifacts artifacts: '**/target/*.jar', followSymlinks: false
                junit '**/target/surefire-reports/TEST*.xml'
                jacoco()   
            }
        }
    }
    post{
        regression {
            emailext body: "${env.BUILD_URL}\\n${currentBuild.absoluteUrl}",
            subject: "${currentBuild.currentResult}: Job ${env.JOB_NAME} [${env.BUILD_NUMBER}]",
            to: 'always@foo.bar'
        }
    }
}
