pipeline {
    agent any

    stages {
        stage ('Compile Stage') {

            steps {
                withMaven(maven : 'maven_4_0_0') {
                    sh 'mvn clean compile'
                }
            }
        }

        stage ('Packaging Stage') {

            steps {
                withMaven(maven : 'maven_4_0_0') {
                    sh 'mvn package'
                }
            }
        }


        stage ('Deployment Stage') {
            steps {
                java -cp target/sample-maven-project-1.0-SNAPSHOT.jar com.sampleproject.mav.App
            }
        }
    }
}
