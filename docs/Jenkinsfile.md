# About our Jenkinsfile

DECOY. This is documentation *about* a pipeline, not a pipeline. Detection must
ignore it on the file extension.

```groovy
pipeline {
    agent any
    stages {
        stage('Build') { steps { sh 'npm ci' } }
    }
}
```
