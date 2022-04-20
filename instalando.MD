 # Instalando o kubectl(ubuntu)
 ~~~linux
 $ sudo apt-get update && sudo apt-get install -y apt-transport-https
 
 $ curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
 
 $ echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee -a /etc/apt/sources.list.d/kubernetes.list
 
 $ sudo apt-get update
 
 $ sudo apt-get install -y kubectl
~~~
# Instalando o Autocompletar do kubectl
### *deve gerar algum script na tela (pra confirmar que tem instalado previsamente o bash-completion):
~~~linux
$ type _init_completion

$ kubectl completion bash >/etc/bash_completion.d/kubectl
~~~~
# Comandos gerais:

* em qual node está cada POD:
~~~~
$ kubectl get pods -o wide 
~~~~
* quantos deployments no cluster:
~~~~
$ kubectl get deployments.apps 
~~~~
* colocar taint num node (só pode ser colocado em nodes):
~~~~
$ kubectl taint nodes <nome-node> key=value:effect
*ex: $ kubectl taint nodes node01 spray=mortein:NoSchedule
~~~~
* como fazer upgrade na master:
** na master faça (ir para master: ssh controlplane):
~~~~
$ apt update
$ apt install kubeadm=1.20.0-00
$ kubeadm upgrade apply v1.20.0

$ apt install kubelet=1.20.0-00 

* precisa restartar kubelet após instalado:
$ systemctl restart kubelet
~~~~

* fornecer acesso a novo membro tedy somente aos nodes:
* * fazer <>.yaml, e então $ kubectl create -f <>.yaml:
~~~~
---
kind: ClusterRole
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  name: node-admin
rules:
- apiGroups: [""]
  resources: ["nodes"]
  verbs: ["get", "watch", "list", "create", "delete"]

---
kind: ClusterRoleBinding
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  name: michelle-binding
subjects:
- kind: User
  name: michelle
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: ClusterRole
  name: node-admin
  apiGroup: rbac.authorization.k8s.io
~~~~
