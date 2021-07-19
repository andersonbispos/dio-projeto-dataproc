
## Breve descrição dos comandos utilizados para resolver o projeto

(comandos executados dentro da Cloud Shell da conta criada pro projeto)

Copiar arquivo do repositorio do git diretamente para o bucket 

```
git clone https://github.com/marcelomarques05/dio-desafio-dataproc
```

```
gsutil cp ~/dio-desafio-dataproc/livro.txt gs://andersonbispos-dio-bucket/
gsutil cp ~/dio-desafio-dataproc/contador.py gs://andersonbispos-dio-bucket/
```


