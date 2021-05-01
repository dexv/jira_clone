<h1 align="center">Implementando Docker + Kubernetes en GCP. Un ejemplo práctico: Clon de Jira construido con React y Node</h1>

<div align="center">Proyecto original de <a href="https://github.com/oldboyxx/jira_clone" target="_blank">oldboyxx/jira_clone</a></div>

<h3 align="center">
  <a href="https://jira.ivorreic.com/">Visitar la aplicación en vivo</a> |
  <a href="https://github.com/oldboyxx/jira_clone/tree/master/client">Ver cliente</a> |
  <a href="https://github.com/oldboyxx/jira_clone/tree/master/api">Ver API</a>
</h3>

![Tech logos](https://i.ibb.co/DVFj8PL/tech-icons.jpg)

![App screenshot](https://i.ibb.co/W3qVvCn/jira-optimized.jpg)

## Crear el namespace y definir namespace creado por defecto

```
cd jira_clone
kubectl apply -f namespaces.yaml
kubectl config set-context --current --namespace=proyecto-final
```

# BackEnd

## Crear secret

Reemplazar los valores de las llaves `DB_HOST` y `DB_PASSWORD`. Para usar este comando en Linux/MacOS se debe reemplazar `^` por `\`

```
kubectl create secret generic jira-credentials ^
    --from-literal=NODE_ENV=development ^
    --from-literal=DB_HOST=192.168.1.84 ^
    --from-literal=DB_PORT=5432 ^
    --from-literal=DB_USERNAME=postgres ^
    --from-literal=DB_PASSWORD=dMwEiidm34234sdfmwei ^
    --from-literal=DB_DATABASE=jira_development ^
    --from-literal=JWT_SECRET=development12345 ^
    -n proyecto-final
```

## Crear imagen

```
cd jira_clone\api
docker build -t node-img .
```

## Ejecutar el deployment

```
cd jira_clone\api
kubectl apply -f deployment.yaml
```

# FrontEnd

## Crear imagen

```
cd jira_clone\client
docker build -t react-img .
```

## Ejecutar el deployment

```
cd jira_clone\client
kubectl apply -f deployment.yaml
```
