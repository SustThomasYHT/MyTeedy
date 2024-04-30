//  pipeline {
//  agent any
//  stages {
//  stage('Build') { 
// steps {
//  sh 'mvn -B -DskipTests clean package' 
// }
//  }
//  }
//  }

// pipeline {
//  agent any
//  stages {
//  stage('Build') { 
// steps {
//  sh 'mvn -B -DskipTests clean package' 
// }
//  }
//  stage('pmd') {
//  steps {
//  sh 'mvn pmd:pmd'
//  }
//  }
//  }
//  post {
//  always {
//  archiveArtifacts artifacts: '**/target/site/**', fingerprint: true
//  archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true
//  archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true
//  }
//  }
//  }



pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                // 使用 Maven 编译项目
                sh 'mvn -B -DskipTests clean package'
            }
        }

        stage('Test') {
            steps {
                // 运行测试并生成 Surefire 报告
                sh 'mvn test'
            }
            post {
                always {
                    // 收集 Surefire 报告
                    junit '**/target/surefire-reports/*.xml'
                }
            }
        }

        stage('Generate JavaDoc') {
            steps {
                // 生成 JavaDoc
                sh 'mvn javadoc:javadoc'
            }
            post {
                always {
                    // 归档生成的 JavaDoc
                    archiveArtifacts artifacts: '**/target/site/apidocs/**/*', fingerprint: true
                }
            }
        }
    }
}
