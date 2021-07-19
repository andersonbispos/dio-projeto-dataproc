
## Breve descrição dos comandos utilizados para resolver o projeto

*(comandos executados dentro da Cloud Shell da conta criada pro projeto)*

- Criar o bucket:


 - Clonar o git do projeto com os arquivos de carga, [livro.txt](https://github.com/andersonbispos/dio-projeto-dataproc/blob/master/desafio/livro.txt) e [contador.py](https://github.com/andersonbispos/dio-projeto-dataproc/blob/master/desafio/contador.py) <- esse contador já é o alterado com os meus parâmetros:

```
git clone https://github.com/marcelomarques05/dio-desafio-dataproc
```
 - Copiar os arquivos da Cloud Shell pro bucket:

```
gsutil cp ~/dio-desafio-dataproc/livro.txt gs://andersonbispos-dio-bucket/
gsutil cp ~/dio-desafio-dataproc/contador.py gs://andersonbispos-dio-bucket/
```
- Criar o cluster dataproc (Haddop) - 1 master e 3 workers:
```
gcloud beta dataproc clusters create cluster-dio-projeto-dataproc --enable-component-gateway --region us-central1 --zone us-central1-a --master-machine-type n1-standard-2 --master-boot-disk-size 500 --num-workers 3 --worker-machine-type n1-standard-2 --worker-boot-disk-size 500 --image-version 2.0-centos8 --optional-components JUPYTER,ZEPPELIN,ZOOKEEPER --project dio-dataproc-lab
```
- Executar o contador.py

```
gcloud dataproc jobs submit pyspark --region us-central1  --cluster=cluster-dio-projeto-dataproc gs://andersonbispos-dio-bucket/contador.py
```
- Clonar o repositorio pra entrega do projeto no cloud shell:
```
git clone https://github.com/andersonbispos/dio-projeto-dataproc
```

- Baixar o arquivo part-00000:
```
gsutil cp gs://andersonbispos-dio-bucket/resultado/part-00000 ~/dio-projeto-dataproc/
```
- Criar o arquivo resultado.txt:

```
head -10 part-00000 > resultado.txt
```

- Publicar o resultado do desafio/projeto:

```
cd dio-projeto-dataproc/ 
git config --global user.email "andersonbispos@gmail.com"
git config --global user.name "Anderson Bispo"
git add * 
git commit -am "submit resultado"
git push origin master
```

### Referências

https://cloud.google.com/sdk/gcloud/reference/dataproc/jobs/submit/pyspark