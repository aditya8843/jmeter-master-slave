pipeline {
  agent any
  stages {
    stage('Print Message') {
      steps {
        echo 'clone'
        sh '''ls 
pwd'''
      }
    }
    stage('Jmeter-Base-Image') {
      steps {
        sh '''cd jmeter-base
docker build --network my-bridge-network --rm --no-cache --tag jmbase .
'''
      }
    }
    stage('Jmeter-Master-Image') {
      steps {
        sh '''cd jmeter-master 
docker build --network my-bridge-network --rm --no-cache --tag vamadhira/jmmaster:v1.0.1 .'''
      }
    }
    stage('Jmeter-Slave-Image') {
      steps {
        sh '''cd jmeter-slave
docker build --network my-bridge-network --rm --no-cache --tag vamadhira/jmserver:v1.0.1 .'''
      }
    }
    stage('Master-Slave-Run') {
      steps {
        sh '''docker run --network my-bridge-network -dit --name slave01 vamadhira/jmserver:v1.0.1 /bin/bash
			  docker run --network my-bridge-network -dit --name slave02 vamadhira/jmserver:v1.0.1 /bin/bash
			  docker run --network my-bridge-network -dit --name slave03 vamadhira/jmserver:v1.0.1 /bin/bash'''
        sh '''docker run  --network my-bridge-network -i -t -d --name master vamadhira/jmmaster:v1.0.1 /bin/bash
ls
pwd
'''
      }
    }
  }
}