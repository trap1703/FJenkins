# FJenkins

#!/bin/env groovy

node{
    deleteDir()
    
    checkout scm
    
    files = sh(returnStdout: true, script: 'ls')
    println "list of property files"
    p_files = files.split("\n").collect()[1,2]
    properties([buildDiscarder(logRotator(numToKeepStr: '100')),
    parameters([choice(choices: p_files, description: 'test test', name: 'param_files')])])
    
    sh 'echo Welcome to IT'
    
}
