pipeline{
	agent {
		label "slave1"
	}
    tools { 
        maven 'maven3'
    }
    stages
       {
            stage("clean")
            {
                steps{
                    sh "mvn clean"
                }
            }
            stage("Build")
            {
                steps{
                    sh "mvn compile"
                }
                
            }
            stage("TEST")
            {
                steps{
                    sh "mvn test"
                }
            }
            stage("package")
            {
                steps{
                    sh "mvn package"
		    sh "pwd"
		    sh "ls -la"
		    sh "ls -R"
			
                }
            } 
	     stage("Deploy")
            {
                steps{
                    sshagent(['ubuntu']){
                    sh "scp -o StrictHostKeyChecking=no   /home/ubuntu/workspace/JenkinsAssignment_production/target/*.jar ubuntu@172.31.81.147:/home/ubuntu/"
                               
                 }
                }
            } 
    }
    post {
        always{
            mail to: 'kirti.ghugtyal@knoldus.com',
			subject: "Pipeline: ${currentBuild.fullDisplayName} is ${currentBuild.currentResult}",
			body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n More info at: ${env.BUILD_URL}"
        }

     }
}
