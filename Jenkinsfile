def label = "test-jnlp"
def cloudId = 'kubernetes'
def namespace = 'default'
podTemplate(
      cloud: cloudId,
      name: label,
      label: label,
      namespace: namespace,
      containers: [
        containerTemplate(
              name: 'jnlp', 
              image: 'jenkins/inbound-agent:4.3-4-alpine',
              args: '${computer.jnlpmac} ${computer.name}',
              workingDir: '/home/jenkins',
              alwaysPullImage: false,
              resourceRequestCpu: '50m',
              resourceLimitCpu: '800m',
              resourceRequestMemory: '512Mi',
              resourceLimitMemory: '1500Mi'
        )
      ]
) {
    node(label){
        stage('github-checkout'){
            container('jnlp'){
                sh 'git version'
                checkout scm
                // checkout([$class: 'GitSCM', branches: [[name: 'main']], doGenerateSubmoduleConfigurations: false, 
                // userRemoteConfigs: [[credentialsId: 'git-checkout-id', url: 'https://github.com/VR1998/sample-repo.git']]])
                sh 'ls -lart'
            }
        }
    }
}