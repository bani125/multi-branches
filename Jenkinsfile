pipeline {
   agent {
		node {
			label "master"
			customWorkspace "/mnt/httpd"
		}
   }
   stages {
		stage ('clone repo') {
			steps {
			sh "rm -rf /mnt/multi-branches"
				sh "git clone https://github.com/bani125/multi-branch.git  -b 22q1"
				sleep 5
				sh "chmod  -R 777 /mnt/multi-branches/index.html"
				sh "scp -i  '/mnt/ohio1.pem' /mnt/multi-branches/index.html  ec2-user@172.31.38.253:/mnt/slave-1/"
			}
		}
		stage ('on slave-1') {
			agent {
				node {
					label  "qa"
					customWorkspace  "/mnt/slave-1"
				}
			}
			steps {
			sh "sudo yum install httpd -y"
				sleep 5
				sh "sudo service httpd start"
				sh "sudo cp -r index.html  /var/www/html"
				sh "sudo chmod -R 777 /var/www/html/index.html"
			}
		}
	}
}


				 
				
