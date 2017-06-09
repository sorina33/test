pipeline {
    agent any
	environment {
	   WORK_DIR = "%HUDSON_HOME%\\workspace\\ci"
	}
    stages {
        stage('Sync sources') {
		    steps {
				echo 'Sync sources'
				bat """
				echo WORK_DIR = %WORK_DIR%
                pushd %WORK_DIR%
                config\\sync.bat
                """
			}
        }
        stage('Compile DB') {
		    steps {
                echo 'Compile DB'
				bat """
                pushd %WORK_DIR%
                config\\compile_DB.bat
                """
			}
        }
       stage('Test DB') {
		    steps {
				parallel ('test_ifs': {
				   bat """
				   pushd %WORK_DIR%
				   config\\test_ifs.bat
				   """ 
				},'test_full_au': {
				   bat """
				   pushd %WORK_DIR%
				   config\\test_full_au.bat
				   """
				})
			}
        }
        stage('Publish DB') {
		    steps {
                echo 'Publish DB'
				bat """
                pushd %WORK_DIR%
                config\\publish_db.bat
                """
			}
        }
    }
}

