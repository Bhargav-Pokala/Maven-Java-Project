#!groovy

node {
    currentBuild.result = "SUCCESS"

    try {

       stage('Checkout'){

          checkout scm
       }

	    stage('Sonar') {
                    //add stage sonar
                    sh 'mvn sonar:sonar'
                }
	
       stage('Compiling'){

          sh 'mvn clean deploy'
       }
	   
          
	stage('Checkstyle') {
                    sh 'mvn checkstyle:checkstyle'
                }

               stage('PMD') {
                    sh 'mvn pmd:check'
                }
	    stage('Tomcat')
	    {
		    // checking purpose
		    sshagent(['549f4f30-c230-4392-bb0a-23cddce7d60b']) {
              sh 'scp -o StrictHostKeyChecking=no target/*.war ec2-user@172.31.27.69:/opt/apache-tomcat-8.0.53/webapps'
    // some block
}

	    }
      /* stage('mail'){

         mail body: 'project build successful',
                     from: 'devopstrainingblr@gmail.com',
                     replyTo: 'mithunreddytechnologies@gmail.com',
                     subject: 'project build successful',
                     to: 'mithunreddytechnologies@gmail.com'
       }*/
	    
	    

    }
    catch (err) {

        currentBuild.result = "FAILURE"

           /* mail body: "project build error is here: ${env.BUILD_URL}" ,
            from: 'devopstrainingblr@gmail.com',
            replyTo: 'mithunreddytechnologies@gmail.com',
            subject: 'project build failed',
            to: 'mithunreddytechnologies@gmail.com'
            */
        throw err
    }
}
