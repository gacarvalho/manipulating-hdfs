
## MANIPULANDO O HDFS 

O objetivo deste respositório é desenvolver um exercício do treinamento da empresa @Semantix. Esse exercício tem como base a manipulação do HDFS (Hadoop Distributed File System) distribuindo por etapas. Vale ressaltar que desafio foi desenvolvido em docker! 

---

📢  ETAPA 1: BAIXAR OS DADOS DO EXERCÍCIO 

  > Questão: Baixar os dados dos exercícios do treinamento

Para baixar os dados do exercício foi necessário realizar um clone do github dentro do caminho ```gabriel@hdgabriel:~/docker-bigdata/input$```
![Etapa 1, imagem 1](https://github.com/gacarvalho/manipulating-hdfs/blob/main/Image/1.png?raw=true)

📢  ETAPA 2: BAIXAR OS DADOS DO EXERCÍCIO 

  > Questão: Acessar o container do namenode

Após baixar a base de dados foi necessário acessar o namenode e listar o seu conteúdo!
![Etapa 2, imagem 2](https://github.com/gacarvalho/manipulating-hdfs/blob/main/Image/2.png?raw=true)

📢  ETAPA 3: BAIXAR OS DADOS DO EXERCÍCIO 

  > Questão: Criar a estrutura de pastas: $ ```user/aluno/seunome/data/recover``` ```user/aluno/seunome/data/delete```

![Etapa 3, imagem 3](https://github.com/gacarvalho/manipulating-hdfs/blob/main/Image/3.png?raw=true)
![Etapa 3, imagem 4](https://github.com/gacarvalho/manipulating-hdfs/blob/main/Image/4.png?raw=true)

📢  ETAPA 4: MOVENDO A PASTA E O ARQUIVO

  > Questão: Enviar a pasta ```/input/exercises-data/escola``` e o arquivo ```/input/exercises-data/entrada1.txt``` para ```data```

Para realizar esse processo foi necessário aplicar o seguinte comando para mover a pasta e depois o arquivo:

```root@namenode:/# hdfs dfs -put /input/exercises-data/escola /user/aluno/gabriel/data```
![Etapa 4, imagem 5](https://github.com/gacarvalho/manipulating-hdfs/blob/main/Image/5.png?raw=true)

Agora podemos conferir o resultado do processo de enviar a pasta:
![Etapa 4, imagem 6](https://github.com/gacarvalho/manipulating-hdfs/blob/main/Image/6.png?raw=true)

```root@namenode:/# hdfs dfs -mv /user/aluno/gabriel/data/entrada1.txt /user/aluno/gabriel/recover```

Depois de mover o arquivo, podemos conferir pelo o comando ```hdfs dfs -ls /user/aluno/gabriel/data```
![Etapa 4, imagem 7](https://github.com/gacarvalho/manipulating-hdfs/blob/main/Image/7.png?raw=true)

📢  ETAPA 5: MOVENDO O ARQUIVO PARA RECOVER

  > Questão: Mover o arquivo “entrada1.txt” para recover
 
Para realizar esse processo vamos aplicar o seguinte comando ```root@namenode:/hdfs dfs -mv /user/aluno/gabriel/data/entrada1.txt /user/aluno/gabriel/recover``` e pela figura abaixo é possível observar que dentro da pasta recover se encontra o arquivo ```entrada1.txt```! E dentro da pasta ```data``` agora se encontra vazia!
![Etapa 5, imagem 9](https://github.com/gacarvalho/manipulating-hdfs/blob/main/Image/9.png?raw=true)
 
📢  ETAPA 6: DELETANDO RECOVER

  > Questão: Deletar a pasta recover

Para realizar a etapa 6 foi necessario aplicar o seguinte comando ```root@namenode:/# hdfs dfs -rm -r /user/aluno/gabriel/recover```, e como é possível observar na imagem abaixo, a pasta recover foi direcionado para a lixeira utilizando o ```TrashPolicyDefault```!
![Etapa 6, imagem 11](https://github.com/gacarvalho/manipulating-hdfs/blob/main/Image/11.png?raw=true)
 
Na figura acima é possível também observar que deletando a pasta com o comando ```-skipTrash```, que tem como objetivo deletar a pasta sem passar pela "lixeira temporária"
  
📢  ETAPA 7: PROCURANDO O ARQUIVO NO HDFS

  > Questão: Procurar o arquivo “alunos.csv” dentro do /user
 
Agora vamos procurar o arquivo ```alunos.csv```  dentro do HDFS e o terminal vai retornar o caminho que se encontra esse arquivo!
![Etapa 7, imagem 12](https://github.com/gacarvalho/manipulating-hdfs/blob/main/Image/12.png?raw=true)
    
📢  ETAPA 8: DETALHANDO O ARQUIVO

  > Questão: Mostrar o último 1KB do arquivo “alunos.csv”
  
Para realizar a etapa 8 foi necessário aplicar o comando ```root@namenode:/# hdfs dfs -tail /user/aluno/gabriel/data/escola/alunos.csv``` e o sistema irá retornar os registro que equivalem a 1KB do arquivo todo.
![Etapa 8, imagem 13](https://github.com/gacarvalho/manipulating-hdfs/blob/main/Image/13.png?raw=true)

📢  ETAPA 9: DETALHANDO OS 5 PRIMEIROS REGISTROS

  > Questão: Mostrar as 5 primeiras linhas do arquivo “alunos.csv”
 
A etapa 9 pede que detalhamos os 5 primeiros registros do arquivos selecionado, para isso vamos aplicar o comando ```root@namenode:/# hdfs dfs -cat /user/aluno/gabriel/data/escola/alunos.csv | head -n 5```
![Etapa 9, imagem 14](https://github.com/gacarvalho/manipulating-hdfs/blob/main/Image/14.png?raw=true)
 
📢  ETAPA 10: VERIFICAÇÃO DA SOMA DAS INFORMAÇÕES

  > Questão: Verificação de soma das informações do arquivo “alunos.csv”

O objetivo principal agora é aplicar um comando que retorne se o arquivo tem consistencia para retornos com put e get. 
![Etapa 10, imagem 15](https://github.com/gacarvalho/manipulating-hdfs/blob/main/Image/15.png?raw=true)
 
📢  ETAPA 11: CRIAÇÃO E REPLICAÇÃO DO ARQUIVO TESTE

  > Questão A: Criar um arquivo em branco com o nome de “test” no data
  > Questão B: Alterar o fator de replicação do arquivo “test” para 2
 
Agora vamos trabalhar com a etapa 11 que pede a criação de um arquivo ```test``` e replicar esse mesmo arquivo para 2  datanode. 
 
Para realizar a questão A vamos aplicar o comando ```root@namenode:/# hdfs dfs -touchz /user/aluno/gabriel/data/teste``` e para vamos consultar com o comando ```root@namenode:/# hdfs dfs -ls /user/aluno/gabriel/data/```
![Etapa 11, imagem 16](https://github.com/gacarvalho/manipulating-hdfs/blob/main/Image/16.png?raw=true)

A questão B pede que replicamos o arquivo teste em 2 datanodes, e para isso vamos aplicar o comando ```root@namenode:/# hdfs dfs -setrep 2 /user/aluno/gabriel/data/teste```! Conforme é possível observar na figura 17, a segunda coluna mostra a quantidade de replicação! Entretanto, concluimos com sucesso essa etapa.
![Etapa 11, imagem 17](https://github.com/gacarvalho/manipulating-hdfs/blob/main/Image/17.png?raw=true)
 
 📢  ETAPA 12: INFORMAÇÕES DO DISCO

  > Questão: Exibir o espaço livre do data e o uso do disco

Agora vamos realizar algumas consultas do arquivo alunos.csv e do disco. O comando ```stat``` permite trazer alguns informações do arquivo, como é demostrado na figura abaixo. 

Para realizar a consulta do disco aplicamos o comando ```root@namenode:/# hdfs dfs -du -h /user/aluno/gabriel/data```, onde é possível observar que a pasta escola tem 29.2M e o arquivo teste com o tamanho 0. 
![Etapa 12, imagem 18](https://github.com/gacarvalho/manipulating-hdfs/blob/main/Image/18.png?raw=true)
