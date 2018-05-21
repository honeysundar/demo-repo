#!groovy

node('master') {

    currentBuild.result = "SUCCESS"

    try {

       stage('Checkout'){
	     echo "SCM checkout"

          checkout scm
       }
       stage('Environment Creation'){
          echo 'This stage will create two RHEL7 ec2 instance with ELB'
          sh 'aws cloudformation create-stack --stack-name TomcatDemoSimpleApp --template-body sample-tomcat-web.json --parameters Subnets=subnet-4ac1ba76,subnet-7b396a1e'
       }

       stage('Application deployment'){

         echo 'Deploy the Sample.war in tomcat'
         sh 'ansible-playbook Application_install.yml'
       }

       stage('Test'){
         echo 'Test the application'
		sh 'curl -O "<CNAME>"/sample/'
       }
    }
    catch (err) {

        currentBuild.result = "FAILURE"

            mail body: "sample application deployment Failure : ${env.BUILD_URL}" ,
            from: 'wills0726@gmail.com',
            replyTo: 'wills0726@gmail.com',
            subject: 'project build failed',
            to: 'wills0726@gmail.com'

        throw err
    }

}


