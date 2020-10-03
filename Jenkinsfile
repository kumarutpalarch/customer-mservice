node () {
        stage ('Code Checkout')
        {
            checkout changelog: false, poll: false, scm: [$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/kumarutpalarch/customer-mservice']]]
        }
        stage ('Build')
        {
            echo "Checkout completed. Starting the build"
            withMaven(maven: 'maven-latest') {
                sh 'mvn clean install package'
                stash name:"jar", includes:"target/customer-service-*.jar"
            }
        }
        stage('unit tests') {
            withMaven(maven: 'maven-latest') {
                sh 'mvn test'   
            }
        }
}
