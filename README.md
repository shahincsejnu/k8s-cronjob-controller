# demo-cronjob-operator


# Flow of this Project

- `cd /home/sahadat/go/src/github.com/shahincsejnu/`
- `mkdir demo-cronjob-operator`
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
- Build Infrastructure:
    - `go.mod`: A new Go module matching our project, with basic dependencies
    - `Makefile`: Make targets for building and deploying your controller
    - `PROJECT`: Kubebuilder metadata for scaffolding new components
    - `config/manager`: launch your controllers as pods in the cluster
    - `config/rbac`: permissions required to run your controllers under their own service account
    - Kubebuilder scaffolds out the basic entrypoint of our project: `main.go`
