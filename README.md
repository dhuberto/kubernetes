# kubernetes - TodoList
![kubernetes](https://img.shields.io/badge/kubernetes-v1.28-326CE5?logo=kubernetes&logoColor=white)
![Kind](https://img.shields.io/badge/Kind-v0.20-000000?logo=kubernetes&logoColor=white)
![NGINX Ingress](https://img.shields.io/badge/NGINX%20Ingress-v1.8-009639?logo=nginx&logoColor=white)
![SQLite](https://img.shields.io/badge/SQLite-v3-003B57?logo=sqlite&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-v24-2496ED?logo=docker&logoColor=white)
![cURL](https://img.shields.io/badge/cURL-v8-073551?logo=curl&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-v18-339933?logo=node.js&logoColor=white)
![Express](https://img.shields.io/badge/Express-v4-000000?logo=express&logoColor=white)

# Laboratório de implantação completa da aplicação manual **TodoList** em um cluster kubernetes (Kind), cobrindo os conceitos de Workloads,Acesso e Persistência de Dados
O **TodoList** é uma aplicação web para gerenciamento de listas de tarefas. Os usuários podem adicionar, concluir e remover itens, contando também com uma rotina automatizada de limpeza periódica via CronJob.

## Baixar o Projeto
```git clone https://github.com/dhuberto/kubernetes.git ```

## Entrar no Projeto
```cd kubernetes ```

# Executar

## Ordem de aplicação dos manifestos

```bash
kubectl apply -f namespace.yaml
kubectl apply -f configmap.yaml
kubectl apply -f secret.yaml
kubectl apply -f pvc.yaml
kubectl apply -f serviceaccount.yaml
kubectl apply -f role.yaml            
kubectl apply -f rolebinding.yaml      
kubectl apply -f deployment.yaml      
kubectl apply -f service.yaml
kubectl apply -f ingress.yaml
kubectl apply -f cronjob.yaml
kubectl apply -f hpa.yaml             
kubectl apply -f pdb.yaml            
```

## Observações

- O Ingress foi configurado utilizando o host:

```
todolist-grupo-02.local
```

Adicione ao arquivo `/etc/hosts`:

```
127.0.0.1 todolist-grupo-02.local
```

- No documento sobre o lab1, o manifesto do CronJob.yml é referenciado a imagem abaixo:

```
curlimages/curl:8
```

Entretanto, essa tag não estava disponível no Docker Hub durante o desenvolvimento do laboratório. Foi utilizada a imagem:

```
curlimages/curl:8.16.0
```

que é compatível com o enunciado e permitiu a execução correta do CronJob.

## Verificações

``` 
kubectl get all,sa,role,rolebinding,hpa,pdb -n todolist-grupo-02
```
## Testar permissões do ServiceAccount

``` 
kubectl auth can-i get pods --as=system:serviceaccount:todolist-grupo-02:todolist-sa -n todolist-grupo-02
```
#
```
kubectl auth can-i delete pods --as=system:serviceaccount:todolist-grupo-02:todolist-sa -n todolist-grupo-02
``` 
## Para atualizar para versão 2
```
git pull origin main
```
## 1. NOVOS recursos (RBAC)
```
kubectl apply -f serviceaccount.yaml
kubectl apply -f role.yaml
kubectl apply -f rolebinding.yaml
```

## 2. ATUALIZAR o Deployment (imagem 1.1.0, probes, resources, serviceAccountName)
```
kubectl apply -f deployment.yaml
```

## 3. NOVOS recursos (HPA e PDB)
```
kubectl apply -f hpa.yaml
kubectl apply -f pdb.yaml
```

## Para acessar o projeto Pelo Browser

``` http://todolist-grupo-02.local ```

## Removendo o projeto

```kubectl delete namespace todolist-grupo-02```
#
```rm -rf ~/kubernetes```

[![Baixar Projeto](https://img.shields.io/badge/Baixar-Projeto-0078D4?logo=github&logoColor=white)](https://github.com/Tiagocamilos/kubernetes/archive/main.zip)


