## Instalar kubectl
- Baixa o kubectl.exe
- Cria uma pasta no C:\kubectl e cola o kubectl.exe na pasta
- Configura uma variavel de ambiente path para a pasta para executar o comando do kubectl de qualquer local do sistema.

## Instalar o AWS CLI
- Baixa o AWS CLI.
- Configura uma Access key no usuário que terá acesso.
- Check se instalou com sucesso. Comando: aws --version
- Configure o AWS CLI com o comando: aws configure
    - Inserir Access key e Secret key
    - Ignorar região e formato de saída.

## Instalar Minikube (Cluster local para testes)
- Baixa o minikube.
- Baixa o virtualbox.
- Ativa virtualização na bios.
- Rodar o comando: minikube start
Será criado um arquivo em %username%/.kube/config. 
    Este é um arquivo de configuração do cluster que o kubectl lê

## Instalar Kind (Cluster local para testes)
- Instala o kind seguindo documentação no site.
- Necessário ter o docker rodando no pc
- Configurar um arquivo de configuração para expor as portas do cluster e informar a quantidade de nós

## Comandos Kubectl
- Ver status do cluster conectado no kubectl, arquivo do ~/.kube/config
```bash
kubectl get svc
```

- Para baixar o arquivo de configuração da aws para o kubectl, é necessário executar o comando abaixo substituindo as variaveis:
```bash
aws eks update-kubeconfig --name nome_do_cluster --region cod_da_regiao
```

- Verifica os nós subindo
```bash
kubectl get nodes --watch
```

Verificar pods
```bash
kubectl get pods
```
```bash
kubectl get pods -o wide
```

Atualiza numero de replicas do deployment
```bash
kubectl scale deployment $deployment_name --replicas=10
```

Ver informações do deployment
```bash
kubectl describe deployment $deployment_name
```

Exporta porta para rede externa de um deployment
```bash
kubectl expose deployment app-html-deployment --type=LoadBalancer --name=app-html --port=80
```

Faz um port-forward para testar um serviço de um deployment especificando a porta do host e a porta do container
```bash
kubectl port-forward svc/$svc_name 80:80
```

Criar arquivo yaml com o deploy com o nome especifico da versao do app no nome do arquivo. Ex: html1.0.yaml e fazer deploy
```bash
kubectl apply -f $arquivo_deploy --record
```

Restaurar versão do deploy
```bash
kubectl rollout undo deploy $deploy
```

Ver versões do deploy que são possiveis restaurar
```bash
kubectl rollout history deploy $deploy
```