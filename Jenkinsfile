pipeline{
    agent any
    stages{
        stage("Build"){
            steps{
                echo "====++++ executing Build... ++++===="
                sh 'npm install'
            }
            post{
                always{
                    echo "====++++ Build Finished! ++++===="
                }
                success{
                    echo "====++++ Build executed succesfully! ++++===="
                }
                failure{
                    echo "====++++ Build execution failed ++++===="
                }
        
            }
        }
        stage("Test"){
            steps{
                echo "====++++ executing Test... ++++===="
                sh 'npm test'
            }
            post{
                always{
                    echo "====++++ Test finished! ++++===="
                }
                success{
                    echo "====++++ Test executed succesfully ++++===="
                }
                failure{
                    echo "====++++ Test execution failed ++++===="
                }
        
            }
        }
        stage("Deploy"){
            steps{
                echo "====++++ executing Deploy... ++++===="
                sh 'nohup npm start > output.log &'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh 'ssh deploy@distractedboyd.ibmlatin.skytapdns.com mkdir -p /home/deploy/desktop/www/prod'
                sh 'scp -r / deploy@distractedboyd.ibmlatin.skytapdns.com:/home/deploy/desktop/www/prod'
                sh 'ssh deploy@distractedboyd.ibmlatin.skytapdns.com cd /home/deploy/desktop/www/prod && npm start'
            }
            post{
                always{
                    echo "====++++ Deploy Finished! ++++===="
                }
                success{
                    echo "====++++ Deploy executed succesfully ++++===="
                }
                failure{
                    echo "====++++ Deploy execution failed ++++===="
                }
        
            }
        }
    }
    post{
        always{
            echo "======== pipeline finished! ========"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}