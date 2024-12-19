# Configuração de Instância EC2 com Volume EBS Adicional

Este repositório documenta o processo de criação de uma instância EC2 t2.micro na AWS, juntamente com a adição e configuração de um novo volume EBS de 8GB.

## Visão Geral

O objetivo deste projeto é demonstrar como adicionar armazenamento persistente a uma instância EC2 usando o Elastic Block Storage (EBS). Um novo volume EBS de 8GB foi criado e anexado à instância, disponibilizando espaço adicional para armazenamento de dados.

## Passos de Configuração

Os seguintes passos foram executados para configurar a instância e o volume:

1.  **Criação da Instância EC2:** Uma instância EC2 t2.micro foi criada na região desejada utilizando o console da AWS ou a AWS CLI.

2.  **Criação do Volume EBS:** Um novo volume EBS de 8GB foi criado na mesma zona de disponibilidade da instância EC2.

3.  **Anexação do Volume EBS:** O volume EBS foi anexado à instância EC2 como `/dev/xvdb`.

4.  **Conexão à Instância:** Conectou-se à instância EC2 via SSH.

5.  **Identificação do Novo Disco:** Utilizou-se o comando `lsblk` para identificar o novo disco `/dev/xvdb`.

    ```bash
    lsblk
    ```

6.  **Formatação da Partição:** Formatou-se a partição criada. Assumindo que a partição criada seja `/dev/xvdb1`, o comando seria:

    ```bash
    sudo mkfs.ext4 /dev/xvdb1
    ```
    (Você pode usar outros sistemas de arquivos como `xfs` se preferir: `sudo mkfs.xfs /dev/xvdb1`)

7.  **Criação do Ponto de Montagem:** Criou-se um diretório para montar o volume:

    ```bash
    sudo mkdir /mnt/data
    ```

8.  **Montagem do Volume:** Montou-se o volume no diretório criado:

    ```bash
    sudo mount /dev/xvdb1 /mnt/data
    ```

9. **Criação de um Arquivo de Teste:** Criou-se um arquivo de teste no volume montado:

    ```bash
    sudo nano /mnt/data/arquivo_de_teste.txt

    ```

## Verificação

Após a configuração, você pode verificar se o volume está montado corretamente executando:

```bash
df -h
