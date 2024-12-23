# Aplicação Dockerizada do WordPress com Nginx, MariaDB e PHP-FPM

Este repositório contém Dockerfiles para configurar uma aplicação WordPress utilizando Nginx, MariaDB e PHP-FPM. A configuração usa o Docker para criar um ambiente com múltiplos containers, facilitando a implantação e escalabilidade.

## Visão Geral

A aplicação consiste em três containers Docker:

1. **MariaDB (Banco de Dados)**
   - Um container MariaDB para armazenar os dados do WordPress.
   - A senha do usuário `root` é configurada como `1234`.
   - Um usuário `user` é criado com a senha `1234` e tem permissões de acesso remoto.
   - Um banco de dados `wordpress` é criado com a codificação de caracteres `utf8mb4` e a colação `utf8mb4_general_ci`.

2. **Nginx (Servidor Web)**
   - O Nginx é configurado para ser o servidor web do WordPress.
   - O Nginx escuta na porta 80.

3. **PHP-FPM (Processamento PHP)**
   - O PHP-FPM processa os arquivos PHP do WordPress.
   - O servidor PHP-FPM escuta na porta 9000.

## Requisitos

- Docker

## Configuração dos Containers

### 1. Container MariaDB

O container MariaDB é configurado para:

- Expor a porta 3306.
- Criar um banco de dados chamado `wordpress` com o conjunto de caracteres `utf8mb4` e colação `utf8mb4_general_ci`.
- Criar o usuário `user`, com acesso remoto (de qualquer host) e a senha `1234`.
- Conceder todas as permissões ao usuário `user` no banco de dados.

### 2. Container Nginx

O container Nginx é configurado para:

- Expor a porta 80.
- Servir o WordPress a partir do diretório `/var/www/html`.
- Baixar e extrair a versão mais recente do WordPress.
- Ajustar a propriedade e as permissões dos arquivos do WordPress.

### 3. Container PHP-FPM

O container PHP-FPM é configurado para:

- Expor a porta 9000.
- Instalar o PHP 8.3 e as extensões necessárias (`php-mysql`, `php-curl`, `php-json`, `php-xml`, `php-mbstring`).
- Configurar o PHP-FPM para escutar na porta `0.0.0.0:9000` para conexões externas.

## Como Executar

### 1. Build e Execução do Container MariaDB

O container MariaDB será configurado para armazenar o banco de dados do WordPress. Ao rodar o container, o banco de dados e o usuário necessário serão criados.

### 2. Build e Execução do Container Nginx

O Nginx servirá o conteúdo do WordPress. O Nginx é configurado para ouvir na porta 80 e servir o WordPress a partir do diretório `/var/www/html`.

### 3. Build e Execução do Container PHP-FPM

O PHP-FPM será responsável por processar os arquivos PHP. Ele será configurado para escutar na porta 9000 e processar as requisições PHP do WordPress.

## Personalizando o WordPress

Você pode personalizar a configuração do WordPress modificando o arquivo `wp-config.php`. Este arquivo será copiado para o container para configurar a instalação do WordPress, principalmente para as configurações de conexão com o banco de dados (nome do host, usuário e senha).

## Parando os Containers

Caso queira parar e remover os containers, basta executar os seguintes comandos para cada container individualmente ou parar todos de uma vez.

## Considerações Finais

- Os containers estão conectados através da rede `wordpress-net`, permitindo a comunicação entre o banco de dados, o servidor web e o processador PHP.
- É importante ajustar o arquivo `wp-config.php` para o ambiente específico, principalmente em relação à configuração de acesso ao banco de dados.
- Os dados do WordPress serão armazenados em um volume Docker (`wordpress_data`), garantindo que os dados persistam mesmo após reinicializações dos containers.

