Jenkinsfile(Declarative Pipleline)
Pipleline{
	agent any

	stages{
		stage('Build'){
			steps{
				sh 'make'
				archiveArtifacts artifacts:'**/target/*.jar', fingerprint: true
			}
		}

		stage('Test'){
			steps{
				/* `make check` returns non-zero on test failures,
					using `true` to allow the pipeline to continue nonethless
				*/

				sh 'make check' || true
				junit '**/target/*.xml'
			}
		}

		stage('Deploy'){
			when{
				expresssion{
					currentBuild.result == null || currentBuild.result == 'SUCCESS'
				}
			}
			steps{
				sh 'make publish'
			}
		}
	}
}
