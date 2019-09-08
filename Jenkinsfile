node{
   
   stage("App Build started"){
      echo 'App build started..'
      git credentialsId: 'Github-ID', url: 'https://github.com/anandbk1/python-docker-app-openshifts.git'
      }
   
   stage('Docker Build') {
     def app = docker.build "anandbk1/py-newrelic"
    }
   
   stage("Tag & Push image"){
      withDockerRegistry([credentialsId: 'dockerID',url: ""]) {
          sh 'docker tag anandbk1/py-newrelic anandbk1/py-newrelic:dev'
          sh 'docker push anandbk1/py-newrelic:dev'
          sh 'docker push anandbk1/py-newrelic:latest'
      }
    }
   
   stage("App deployment started"){
     sh 'oc login --token=DPwoijGmkVpymA7qqIMMJI3g3niQqUTpDvzg-aQ2sCw --server=https://api.us-west-1.starter.openshift-online.com:6443'
     sh 'oc project jenkin-openshift'
     //sh 'oc new-app --name py-anand anandbk1/py-newrelic'
      sh 'oc rollout latest dc/py-newrelic -o json' 
     //sh 'oc expose svc py-mani' 
    }
   
    stage('App deployed to Openshift environment') {
     echo 'App deployed to Openshift environment..'
    }

  }
