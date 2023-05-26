### FRANCISCO JAIME DA SILVA


# Desafio GCP Dataproc

Código criado para utilização junto a plataforma da Digital Innovation One

<p align="center"><img src="./DIO.png" width="500"></p>

## Desafio GCP Dataproc
## Google Cloud

__*Foi Criando um ecossistema Hadoop totalmente gerenciado com Google Cloud Platform*__

O desafio consistia em efetuar um processamento de dados utilizando o produto Dataproc do GCP. Esse processamento deveira efetuar a contagem das palavras de um livro e informar quantas vezes cada palavra aparecia no mesmo.

---

### Etapas do Desafio

1. Foi Criado um bucket no Cloud Storage com o nome **bddio**
1. Foi Atualizdo o arquivo 'contador.py' com o nome do Bucket criado. Ficand assim:<br />
  import sys <br />
  from pyspark import SparkContext, SparkConf <br />
  if __name__ == "__main__":<br />
      sc = SparkContext("local","PySpark Exemplo - Desafio Dataproc")<br />
      words = sc.textFile("gs://bddio/livro.txt").flatMap(lambda line: line.split(" "))<br />
      wordCounts = words.map(lambda word: (word, 1)).reduceByKey(lambda a,b:a +b).sortBy(lambda a:a[1], ascending=False)<br />
      wordCounts.saveAsTextFile("gs://bddio/resultado")<br />
2. Foi feito o upload dos arquivos 'contador.py' e 'livro.txt' para o bucket criado (instruções abaixo)
    - https://cloud.google.com/storage/docs/uploading-objects

1. Foi Utilizado o código em um cluster Dataproc, executando um Job do tipo PySpark chamando 'gs://bddio/contador.py'
1. O Job gerou uma pasta no bucket chamada 'resultado' e dentro dessa pasta o arquivo 'part-00000' contendo a lista de palavras e quantas vezes elas se repetirm em todo o livro.


