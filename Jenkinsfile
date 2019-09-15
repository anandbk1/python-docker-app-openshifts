node{
   
   stage("App Build started"){
      echo 'App build started..'
      git credentialsId: 'Github-ID', url: 'https://github.com/anandbk1/python-docker-app-openshifts.git'
      }
   
   stage('Docker Build') {
     def app = docker.build "anandbk1/python-relic"
    }
   
   stage("Tag & Push image"){
      withDockerRegistry([credentialsId: 'dockerID',url: ""]) {
          sh 'docker tag anandbk1/python-relic anandbk1/python-relic:dev'
          sh 'docker push anandbk1/python-relic:dev'
          sh 'docker push anandbk1/python-relic:latest'
      }
    }
   
   stage("App deployment started"){
     sh 'oc login --token=AUeAqkp8CQOqlTgbqbSv_PlvL_TxuDGQbtqDVtRQRvE --server=https://api.us-west-1.starter.openshift-online.com:6443'
     sh 'oc project pyrelic'
     sh 'oc new-app --name pyrelic anandbk1/python-relic'
      sh 'oc rollout latest dc/pyrelic -o json' 
     sh 'oc expose svc py-relic' 
    }
   
    stage('App deployed to Openshift environment') {
     echo 'App deployed to Openshift environment..'
    }

  }
