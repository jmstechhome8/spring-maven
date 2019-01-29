node {
   def mvnHome
   stage('getscm') { // for display purposes
      // Get some code from a GitHub repository
      git 'https://github.com/ybmadhu/spring3-mvc-maven-xml-hello-world.git'
      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured
      // **       in the global configuration.           
      mvnHome = tool 'Maven'
   }
   stage('Build') {
      // Run the maven build
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
      } else {
         bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
      }
   }
    stage('artifact') {
      
      archive 'target/*.war'
   }
   stage ('deploy'){
       bat '''copy C:\\Users\\Madhu\\.jenkins\\workspace\\kelly_pipeline_java_maven\\target\\*.war F:\\softwares\\apache-tomcat-7.0.53\\webapps\\'''
   }
}
