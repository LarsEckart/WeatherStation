node {
  stage('Checkout') {
        checkout scm
  }

  stage('Build') {
        sh "./gradlew clean assemble test check jacocoTestReport"
  }

  stage('Report') {
        androidLint canComputeNew: false, defaultEncoding: '', healthy: '', pattern: '**/lint-results.xml', unHealthy: '', unstableTotalAll: '0'
        step([$class: 'CheckStylePublisher', canComputeNew: false, defaultEncoding: '', healthy: '', pattern: '**/reports/**/detekt.xml', unHealthy: '', unstableTotalAll: '0'])
        junit '**/test-results/debug/junit-platform/*.xml'
        jacoco exclusionPattern: '**/R.class, **/R$*.class, **/*$ViewInjector*.*, **/BuildConfig.*, **/Manifest*.*, **/*Test*.*, android/**/*.*, androidx/**/*.*, **/*Fragment.*, **/*Activity.*', classPattern: '**/classes, **/tmp/kotlin-classes/debug'
  }
}
