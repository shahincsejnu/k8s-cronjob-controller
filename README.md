# k8s-cronjob-controller

- live running codes of this project here: https://github.com/kubernetes-sigs/kubebuilder/tree/master/docs/book/src/cronjob-tutorial/testdata/project
I just tried to recreate this project, still not finished.
- followed this [tutorial](https://book.kubebuilder.io/cronjob-tutorial/cronjob-tutorial.html)

## Basics

- The job of the CronJob controller is to run one-off tasks on the kubernetes cluster at regular intervals.
- It does this by building on top of the Job controller, whose task is to run one-off tasks once, seeing them to completion.

# Flow of this Project

- `cd /home/sahadat/go/src/github.com/shahincsejnu/`
- `mkdir k8s-cronjob-controller`
- `go mod init`
- installed kubebuilder through commands (and also clone the kubebuilder repo and create the controller-gen binary)
    - ```shell script
      os=$(go env GOOS)
      arch=$(go env GOARCH)
    
      # download kubebuilder and extract it to tmp
      curl -L https://go.kubebuilder.io/dl/2.3.2/${os}/${arch} | tar -xz -C /tmp/
    
      # move to a long-term location and put it on your path
      # (you'll need to set the KUBEBUILDER_ASSETS env var if you put it somewhere else)
      sudo mv /tmp/kubebuilder_2.3.2_${os}_${arch} /usr/local/kubebuilder
      export PATH=$PATH:/usr/local/kubebuilder/bin
      ```
      If from inside your project or from `fish`, `kubebuilder` is not found then first do `export PATH=$PATH:/usr/local/kubebuilder/bin`
- scaffold out this new project
    - `kubebuilder init --domain tutorial.kubebuilder.io`: we'll use a domain of tutorial.kubebuilder.io, so all API groups will be <group>.tutorial.kubebuilder.io.
- `kubebuilder create api --group batch --version v1 --kind CronJob`: To scaffold out a new Kind and corresponding controller, we can use kubebuilder create api. The first time we call this command for each group-version, it will create a directory for the new group-version. Each time we call the command with a different kind, it’ll add a corresponding new file.



## Build Infrastructure

- `go.mod`: A new Go module matching our project, with basic dependencies
- `Makefile`: Make targets for building and deploying your controller
- `PROJECT`: Kubebuilder metadata for scaffolding new components
- `config/manager`: launch your controllers as pods in the cluster
- `config/rbac`: permissions required to run your controllers under their own service account
- Kubebuilder scaffolds out the basic entrypoint of our project: `main.go`


# Intuitions

- We run our `manager`, which in turn runs all of our controllers and webhooks. The manager is set up to run until it receives a graceful shutdown signal. 
