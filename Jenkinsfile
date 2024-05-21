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



// pipeline {
//     agent any

//     stages {
        
//         stage('Build') {
//             steps {
//                 // 使用 Maven 编译项目
//                 sh 'mvn -B -DskipTests clean package -U'
//             }
//         }

//         stage('Test') {
//             steps {
//                 // 运行测试并生成 Surefire 报告
//                 sh 'mvn test'
//             }
//             post {
//                 always {
//                     // 收集 Surefire 报告
//                     junit '**/target/surefire-reports/*.xml'
//                 }
//             }
//         }

//         stage('Generate JavaDoc') {
//             steps {
//                 // 生成 JavaDoc
//                 sh 'mvn clean -DskipTests install'
//                 sh 'mvn javadoc:jar -U'
//             }
//             post {
//                 always {
//                     // 归档生成的 JavaDoc
//                     archiveArtifacts artifacts: '**/target/apidocs/**/*', fingerprint: true
//                 }
//             }
//         }
//     }
// }




// pipeline {
//     agent any

//     stages {
        
//         stage('Build') {
//             steps {
//                 // 使用 Maven 编译项目
//                 sh 'mvn -B -DskipTests clean package -U'
//             }
//         }
//         stage('Building image') {
//             steps {
//                 // 生成 JavaDoc
//                 sh 'mvn clean -DskipTests install'
//                 sh 'docker build -t teedy2024_lab12_1 .'
//             }
//         }

//         stage('Upload image') {
//             steps {
//                 // 生成 JavaDoc
//                 sh 'docker tag teedy2024_lab12 thomasyht1728/teedy_lab12_1:v2.0'
//                 // sh 'docker push thomasyht1728/teedy_lab12_1:v2.0'
//             }
//         }

//         stage('Run containers') {
//             steps {
//                 // 生成 JavaDoc
//                 sh 'docker run -d -p 8084:8080 --name teedy_lab12_01_2 teedy2024_lab12_1'
//                 sh 'docker run -d -p 8083:8080 --name teedy_lab12_02_2 teedy2024_lab12_1'
//                 sh 'docker run -d -p 8082:8080 --name teedy_lab12_03_2 teedy2024_lab12_1'
//             }
//         }
//     }
// }

pipeline {
         agent any
        
         stages {
                 stage('Build') { 
                        steps {
                                 sh 'mvn -B -DskipTests clean package' 
                        }
                 }
                 stage('K8s') {
                         steps {
                                 sh 'kubectl set image deployments/hello-node docs=6278fbea197f'
                         }
                }
         }
 }
