node("Master")
 {
     def branchName = "master"
	 stage("SCM")
	 {
	      checkout scm
		  echo "Branch = (${branchName})"
	 }
	 
   stage('Environment Creation")
      def AwsHOme = tool '/bin/'
         withEnv(["PATH+AWS=${tool '/bin/aws'}]"])
          {
		     sh 'aws cloudformation create-stack --stack-name TomcatDemoSimpleApp --template-body sample-tomcat-web.json --parameters Subnets=subnet-4ac1ba76,subnet-7b396a1e'
		  }		 
  }
   stage("Application deployment")
      {
	     withEnv(["PATH+ANSIBLE=${tool '/usr/bin/"}])
		   {
		      sh 'ansible-playbook Application_install.yml'
		   }
	  
	  }
   stage("Test")
      {
	   withEnv(["PATH+AWS+AWS=${tool '/bin/aws"}])
		   {
		      sh 'curl -O "<CNAME>"/sample/'
		   }
	 
	  }