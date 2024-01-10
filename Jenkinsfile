pipeline {
	agent any
	stages {
		stage('Build') {
			steps {
				sh 'pip3 install -r requirements.txt'
			}
		}
		stage('Test') {
			steps {
				sh 'python3 manage.py test'
			}
		}
		stage('Deploy') {
			steps {
				sh 'ssh -o StrictHostKeyChecking=no deployment-user@app-server "source denv/bin/activate; \
				cd polling; \
				git pull origin main;\
				pip3 install -r requirements.txt --no-warn-script-location; \
				python3 manage.py migrate; \
				deactivate; \
				sudo systemctl restart nginx; \
				sudo systemctl restart gunicorn "'
			}
		}
	}
}
