pipeline {
	agent any
	stages {

		stage('Lint HTML') {
			steps {
				sh 'tidy -q -e *.html'
			}
		}$class: 'AmazonWebServicesCredentialsBinding'
		
		stage('Build Docker Image') {
			steps {
				withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'udacity_capstone', usernameVariable: 'anuguptaudacity', passwordVariable: 'udacity@anu1']]){
					sh '''
						docker build -t anuguptaudacity/capstone .
					'''
				}
			}
		}

		stage('Push Image To Dockerhub') {
			steps {
				withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'udacity_capstone', usernameVariable: 'anuguptaudacity', passwordVariable: 'udacity@anu1']]){
					sh '''
						docker login -u anuguptaudacity -p udacity@anu1
						docker push anuguptaudacity/capstone
					'''
				}
			}
		}

		stage('Set current kubectl context') {
			steps {
				withAWS(region:'us-east-1', credentials:'udacity_capstone') {
					sh '''
						kubectl config use-context arn:aws:eks:us-east-1:142977788479:cluster/capstonecluster
					'''
				}
			}
		}

		stage('Deploy blue container') {
			steps {
				withAWS(region:'us-east-1', credentials:'udacity_capstone') {
					sh '''
						kubectl apply -f ./blue-controller.json
					'''
				}
			}
		}

		stage('Deploy green container') {
			steps {
				withAWS(region:'us-east-1', credentials:'udacity_capstone') {
					sh '''
						kubectl apply -f ./green-controller.json
					'''
				}
			}
		}

		stage('Create the service in the cluster, redirect to blue') {
			steps {
				withAWS(region:'us-east-1', credentials:'udacity_capstone') {
					sh '''
						kubectl apply -f ./blue-service.json
					'''
				}
			}
		}

		stage('Wait user approve') {
            steps {
                input "Ready to redirect traffic to green?"
            }
        }

		stage('Create the service in the cluster, redirect to green') {
			steps {
				withAWS(region:'us-east-1', credentials:'udacity_capstone') {
					sh '''
						kubectl apply -f ./green-service.json
					'''
				}
			}
		}

	}
}
