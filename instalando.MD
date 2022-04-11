### Instalando o kubectl(ubuntu)

$ sudo apt-get update && sudo apt-get install -y apt-transport-https
$ curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
$ echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee -a /etc/apt/sources.list.d/kubernetes.list
$ sudo apt-get update
$ sudo apt-get install -y kubectl

## Instalando o Autocompletar do kubectl
 # deve gerar algum script na tela(pra confirmar que tem instalado previsamente o bash-completion):
$ type _init_completion

$ kubectl completion bash >/etc/bash_completion.d/kubectl


### comandos gerais:

# em qual node está cada POD:
~~~~kubernetes
$ kubectl get pods -o wide 


# colocar taint num node (só pode ser colocado em nodes):
$ kubectl taint nodes <nome-node> key=value:effect
ex:
$ kubectl taint nodes node01 spray=mortein:NoSchedule
