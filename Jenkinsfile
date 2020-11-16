pipeline{
    agent any
    tools {
        maven "maven3"
    }
    stages{
        stage('get scm'){
            steps{
                git credentialsId: 'github_credentials', url: 'https://github.com/jmstechhome8/spring3-mvc-maven-xml-hello-world.git'
            }
        }
        stage('maven build'){
            steps{
               sh "mvn package"
            }
        }
        stage('archive artifact'){
            steps{
                archiveArtifacts artifacts: '**/target/*.war', followSymlinks: false
            }
            
        }
        stage('deploy'){
            steps{
                
                withCredentials([usernameColonPassword(credentialsId: 'tomcat_credentials', variable: 'tomcatcredentails')]) {

                  sh "curl -v -u tomcatcredentails -T /var/lib/jenkins/workspace/end-to-end-automation/target/spring3-mvc-maven-xml-hello-world-1.3.war 'http://ec2-13-126-144-239.ap-south-1.compute.amazonaws.com:8080/manager/text/deploy?path=/pipeline_spring&update=true'"
                }
            }
        }
        
    }
    
     post {
        failure {
            script {
                currentBuild.result = 'FAILURE'
            }
        }

        always {
            step([$class: 'Mailer',
                notifyEveryUnstableBuild: true,
                recipients: "jmstechhome@gmail.com",
                sendToIndividuals: true])
        }
    }
}
