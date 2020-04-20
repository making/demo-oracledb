

```
cf create-service credhub default -c '{"url":"oracle://<username>:<password>@<hostname>:<port>/<sid>"}'
```

or 

```
cf create-user-provided-service demo-db -p '{"url":"oracle://<username>:<password>@<hostname>:<port>/<sid>"}'
```


```
cf push
```