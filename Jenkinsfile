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

    tools {
        // 确保你安装了 Maven，并在 Jenkins 配置中设置了 MAVEN_HOME 
        maven 'Maven3'
    }

    stages {
        stage('Checkout') {
            steps {
                // 获取最新的代码
                checkout scm
            }
        }

        stage('Build') {
            steps {
                // 使用 Maven 编译项目
                sh 'mvn clean compile'
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

        // stage('Deploy') {
        //     steps {
        //         // 这里添加你的部署脚本，如果有的话
        //         echo 'Deploying'
        //     }
        // }
    }
}
