# 1° Passo -> 

Criar estrutura de pastas pasta

D:\ 
|------Kafka	
|---------application
|------------Conteudo (Colar conteudo da pasta de DOWNLOAD Aqui)
|---------data
|------------zookeeper
|---------tmp
|------------kafka-logs
|---------------1
|---------------2
|---------batch

Ou se prefereir, abrir o Prompt de comando e executar os seguintes comandos (pressione WIN + R, escreva cmd e aperte enter):

    D:
    mkdir D:\Kafka
    mkdir D:\Kafka\application
    mkdir D:\Kafka\data
    mkdir D:\Kafka\data\zookeeper
    mkdir D:\Kafka\tmp
    mkdir D:\Kafka\tmp\kafka-logs
    mkdir D:\Kafka\tmp\kafka-logs\1
    mkdir D:\Kafka\tmp\kafka-logs\2
    mkdir D:\Kafka\batch

Caso o seu Disco Local não seja particionado, e você apenas possua um, utilize "C: "	

---

# 2° Passo ->

Download no site https://kafka.apache.org/downloads

Extrair arquivo baixado e copiar o conteudo para D:\Kafka\application/Conteudo

---

# 3° Passo ->

Abrir pasta D:\Kafka\application\config\
copiar arquivo server.properties e colar duas vezes o mesmo conteudo e renomear com os nomes abaixo
- server1.properties 
- server2.properties

# 4° Passo ->

Editar arquivo D:\Kafka\application\config\server1.properties
- Setar broker id = 1 

        broker.id=1

- Descomentar a linha e setar porta 9092 para o server1

        listeners=PLAINTEXT://:9092

- Setar diretório de logs para o diretório criado para o server1

        D:/Kafka/tmp/kafka-logs/1

- Numero de partições por topico setar 2

        num.partitions=2 

# 5° Passo ->

Editar arquivo D:\Kafka\application\config\server2.properties
- Setar broker id = 2

        broker.id=2

- Descomentar a linha e setar porta 9093 para o server1

        listeners=PLAINTEXT://:9093

- Setar diretório de logs para o diretório criado para o server1

        D:/Kafka/tmp/kafka-logs/2

- Numero de partições por topico setar 2

        num.partitions=2 

# 6° Passo ->

Editar o arquivo D:\Kafka\application\config\zookeeper.properties

- Setar o diretorio de dados(datadir) para o zookeeper

        dataDir=D:/Kafka/data/zookeeper

# 7° Passo ->

Abra o Prompt de comando e execute os comandos a seguir:

Batch para Inicializar o Zookeeper e Kafka cluster

    echo start D:\Kafka\application\bin\windows\zookeeper-server-start.bat D:\Kafka\application\config\zookeeper.properties > D:\Kafka\batch\Start_Zookeeper.bat

Batch para Inicializar o Servidor 1 Kafka

    echo start D:\Kafka\application\bin\windows\kafka-server-start.bat D:\Kafka\application\config\server1.properties > D:\Kafka\batch\Start_Kafka_Server1.bat

Batch para Inicializar o Servidor 2 Kafka

    echo start D:\Kafka\application\bin\windows\kafka-server-start.bat D:\Kafka\application\config\server2.properties > D:\Kafka\batch\Start_Kafka_Server2.bat

# 8° Passo ->

Abra as batchs criadas para inicializar o cluster

- Start_Zookeper.bat
- Start_Kafka_Server1.bat
- Start_Kafka_Server2.bat

# 9° Passo ->

Vamos criar dois topicos para teste

Batch para criar topico customer

    echo start D:\Kafka\application\bin\windows\kafka-topics.bat --create --zookeeper localhost:2181 --replication-factor 2 --partitions 2 --topic customer_topic > D:\Kafka\batch\Create_customer_topic.bat

Batch para criar topico product

    echo start D:\Kafka\application\bin\windows\kafka-topics.bat --create --zookeeper localhost:2181 --replication-factor 2 --partitions 2 --topic product_topic > D:\Kafka\batch\Create_product_topic.bat


# 10° Passo -> 

Vamos agora, iniciar o serviço de producer e consumer, para assim podermos enviar e receber mensagens atraves do kafka broker (customer_topic)

Batch para inicializar o serviço de producer para o topico customer_topic

    echo start D:\Kafka\application\bin\windows\kafka-console-producer.bat --topic customer_topic --broker-list localhost:9092,localhost:9093 > D:\Kafka\batch\Producer_customer_topic.bat

Vamos agora, criar a batch para iniciar o serviço de consumer, par aassim podermos receber mensagens do kafka broker (customer_topic)

    echo start D:\Kafka\application\bin\windows\kafka-console-consumer.bat --bootstrap-server localhost:9092 --from-beginning --topic customer_topic > D:\Kafka\batch\Consumer_customer_topic.bat

# 11° Passo -> 

Vamos, iniciar o serviço de producer e consumer, para assim podermos enviar e receber mensagens atraves do kafka broker (product_topic)

Batch para inicializar o serviço de producer para o topico product_topic

    echo start D:\Kafka\application\bin\windows\kafka-console-producer.bat --topic product_topic --broker-list localhost:9092,localhost:9093 > D:\Kafka\batch\Producer_product_topic.bat

Vamos, criar a batch para iniciar o serviço de consumer, par aassim podermos receber mensagens do kafka broker (product_topic)

    echo start D:\Kafka\application\bin\windows\kafka-console-consumer.bat --bootstrap-server localhost:9092 --from-beginning --topic product_topic > D:\Kafka\batch\Consumer_product_topic.bat

--------------------------------------------------------------------------------------------------------------------------------------------------------------

# 12° Passo ->

Vamos Verificar e descrever o status dos topicos do kafka

Batch para descrever o status do kafka para o topico customer_topic

    echo start D:\Kafka\application\bin\windows\kafka-topics.bat --describe --zookeeper localhost:2181 --topic customer_topic > D:\Kafka\batch\Status_customer_topic.bat

Batch para descrever o status do kafka para o topico product_topic

    echo start D:\Kafka\application\bin\windows\kafka-topics.bat --describe --zookeeper localhost:2181 --topic product_topic > D:\Kafka\batch\Status_product_topic.bat

---

# Fim !! 

Se você chegou até o final e obteve êxito, parabéns ! você ja é capaz de implementar o apache kafka em ambiente windows\kafka-console-consumer


Matheus Pavanetti
matheuspavanetti@gmail.com
23/07/2020
