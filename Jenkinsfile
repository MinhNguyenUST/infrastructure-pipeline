properties([pipelineTriggers([githubPush()])])

node('linux') {
    git url: 'https://github.com/MinhNguyenUST/infrastructure-pipeline.git', branch: 'master'
    stage('Test') {
        sh "env"
    }
	
	stage ("GetInstances") {

        sh "aws ec2 describe-instances --region us-east-1"
    }
	
	stage ("CreateInstance") {
        // TODO
		//sh "aws ec2 run-instances --image-id ami-0f830c70 --count 1 --instance-type t2.micro --key-name SEIS665_KeyPair --security-group-ids sg-093653d41a3fe2c9c --subnet-id subnet-0648f7611b25f1ef0 --region us-east-1"
		//def output = sh returnStdout: true, script: 'aws ec2 describe-instances | jq .Instances[0].InstanceId' 
		//echo "${output}"
		
		sh "aws ec2 run-instances --image-id ami-013be31976ca2c322 --count 1 --instance-type t2.micro --key-name SEIS665_KeyPair --security-group-ids sg-ffc4f1b3 --subnet-id subnet-ff6b13f0 --region us-east-1"
		def output = sh returnStdout: true, script: 'aws ec2 describe-instances --region us-east-1 | jq .Instances[0].InstanceId' 
		sh "aws ec2 wait --region us-east-1 instance-running --instance-ids ${output}"
		sh "aws ec2 terminate-instances --region us-east-1 --instance-ids ${output}"
    }
}