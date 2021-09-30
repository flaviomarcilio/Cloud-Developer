# Desenvolvimento em Cloud

## Desafio GCP Dataproc

Este desafio faz parte do curso na plataforma da Digital Innovation One:

__*Criando um ecossistema Hadoop totalmente gerenciado com Google Cloud Patform*__

apresentado por Marcelo Marques. O repositório base pode ser encontrado [aqui](https://github.com/marcelomarques05/dio-desafio-dataproc)

---
### Etapas do Desafio

1. Criar um bucket no Cloud Storage:

    **buckets** são contêineres básicos que armazenam dados no Cloud Storage. Para criar o *bucket*, primeiro, é necessário criar um projeto ou selecionar um existente e ativar o faturamento para este projeto. Após selecionar o projeto, o *bucket* pode ser criado com o seguinte comando na *Cloud shell*
    ```shel
    gsutil mb -b on -l us-east1 gs://my-bucket/
    ```
    Este comando cria um bucket chamado *"my-bucket"*. Outras maneiras de criar *buckets* podem ser encontradas em:
     - https://cloud.google.com/storage/docs/creating-buckets?hl=pt-br

2. Atualizar o arquivo ```contador.py``` com o nome do *bucket* criado nas linhas que contém ```{SEU_BUCKET}```:

    Os arquivos desse desafio são obtidos fazendo o clone do [repositório base](https://github.com/marcelomarques05/dio-desafio-dataproc) na *Cloud shell* do projeto.

3. Fazer o upload dos arquivos ```contador.py``` e ```livro.txt``` para o *bucket* criado:
   
    Utilizando a *Cloud shell*:

    ```shell
    gsutil cp contador.py livro.txt gs://my-bucket/
    ```

    Ou seguindo os passos descritos em:
     - https://cloud.google.com/storage/docs/uploading-objects?hl=pt-br#console

4. Utilizar o código em um cluster Dataproc, executando um Job do tipo PySpark chamando ```gs://my-bucket/contador.py```

    Utilizando a *Cloud shell*:

    ```shell
    gcloud dataproc jobs submit pyspark \
    gs://my-bucket/contador.py \
    --cluster=cluster-name  \
    --region=region
    ```

5. O Job irá gerar uma pasta no bucket chamada ```resultado```. Dentro dessa pasta o arquivo ```part-00000``` irá conter a lista de palavras e quantas vezes ela é repetida em todo o livro.

### Resultados

1. Dentro de [resultado.txt](resultado.txt), tem as 10 palavras que mais são usadas no livro, de acordo com o resultado do Job.
2. O arquivo [resultado_part-00000](resultado_part-00000) é o arquivo completo gerado pelo processamento do livro.
---