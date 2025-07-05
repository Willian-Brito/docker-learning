# 🐳 Introdução ao Docker

<div align="center">
  <img src="https://raw.githubusercontent.com/Willian-Brito/docker-learning/refs/heads/main/prints/docker_logo.svg.png" />
</div>

## 📌 O que é ?

Docker é uma plataforma de código aberto que permite empacotar, distribuir e executar aplicações em **containers**. Um container é uma unidade leve e portátil que contém tudo o que uma aplicação precisa para funcionar, como código, bibliotecas, dependências e variáveis de ambiente, garantindo que ela seja executada da mesma forma em qualquer ambiente.


## ⚙️ Como funciona?

Docker utiliza a funcionalidade de **containers do kernel Linux** (namespaces e cgroups) para isolar aplicações, proporcionando um ambiente leve e consistente, diferente de uma máquina virtual completa.

A arquitetura do Docker pode ser dividida em quatro partes principais:

1. **Docker Engine**  
   O serviço principal que roda em segundo plano. Ele é responsável por criar, executar e gerenciar containers.
   <div align="center">
      <img src="https://raw.githubusercontent.com/Willian-Brito/docker-learning/refs/heads/main/prints/docker_engine.png" height="300
      " />
   </div>

2. **Docker Images**  
   Imagens são templates imutáveis com tudo que um container precisa. Você pode pensar nelas como snapshots do ambiente da aplicação.
   <div align="center">
      <img src="https://raw.githubusercontent.com/Willian-Brito/docker-learning/refs/heads/main/prints/Imagens%20docker.png" height="300" />
   </div>

3. **Docker Containers**  
   São instâncias executáveis baseadas nas imagens. Podem ser criadas, iniciadas, paradas e removidas de forma rápida.
   <div align="center">
      <img src="https://raw.githubusercontent.com/Willian-Brito/docker-learning/refs/heads/main/prints/docker_container.png" height="300" />
   </div>

4. **Dockerfile**  
   É um arquivo que define como a imagem do container deve ser construída, especificando base, comandos, cópias, portas e variáveis.

## 🆚 Docker vs. Máquinas Virtuais (VMs)

| Característica          | Docker (Containers)                          | Máquinas Virtuais (VMs)                        |
|------------------------|---------------------------------------------|-----------------------------------------------|
| **Isolamento**         | Compartilham o kernel do host                | Cada VM possui seu próprio sistema operacional |
| **Desempenho**         | Mais leve e rápido                           | Mais pesado e com maior consumo de recursos    |
| **Inicialização**      | Em segundos                                  | Em minutos                                     |
| **Imagens**            | Leves (geralmente < 1GB)                     | Pesadas (várias GBs)                           |
| **Portabilidade**      | Altamente portátil                           | Menos portátil                                 |
| **Overhead**           | Mínimo                                       | Considerável                                   |
| **Segurança**          | Isolamento menor (compartilha kernel)        | Isolamento mais robusto                        |
| **Uso principal**      | Microserviços, CI/CD, DevOps, cloud-native   | Aplicações legadas, ambientes full-stack       |


**Exemplo:**
<div align="center">
   <img src="https://raw.githubusercontent.com/Willian-Brito/docker-learning/refs/heads/main/prints/docker%20vs%20vm.png" height="400" />
</div>

## 🏗️ Arquitetura

A arquitetura do Docker é baseada em um modelo cliente-servidor que permite o controle e gerenciamento de containers. Ela é composta por três elementos principais:

<div align="center">
   <img src="https://raw.githubusercontent.com/Willian-Brito/docker-learning/refs/heads/main/prints/docker_arquitetura.png" height="400" />
</div>


### 🔳 1. Docker CLI (Cliente)

O **Docker CLI** (`docker`) é a interface de linha de comando usada para interagir com o Docker Engine. É por meio dela que desenvolvedores executam comandos como `docker build`, `docker run`, `docker pull`, entre outros.

### 🖥 2. Docker Engine (Servidor)

O **Docker Engine** é o coração do Docker. Ele é composto por três partes:

- **Docker Daemon (`dockerd`)**  
  Responsável por construir, executar e gerenciar containers, imagens e volumes. Ele escuta requisições da API e executa os comandos solicitados.

- **API REST**  
  Uma interface HTTP que o cliente Docker utiliza para se comunicar com o daemon. Essa API pode ser acessada por outros aplicativos, além do CLI.

- **Container Runtime (containerd)**  
  Um componente responsável pela execução efetiva dos containers. Ele gerencia o ciclo de vida dos containers de forma isolada e eficiente.

### ⛁ 3. Docker Registry

O **Docker Registry** é o repositório de imagens. O mais conhecido é o [Docker Hub](https://hub.docker.com), mas é possível hospedar registries privados. Comandos como `docker push` e `docker pull` interagem diretamente com esse serviço.

### 🔄 Fluxo de Funcionamento

1. O desenvolvedor usa o `Docker CLI` para enviar um comando.
2. O `Docker CLI` se comunica com o `Docker Daemon` via API.
3. O `Daemon` executa a ação solicitada: construir imagem, iniciar container, etc.
4. O `Docker Daemon` pode buscar imagens de um registry, como o Docker Hub.
5. O container é criado ou iniciado com base na imagem.

### 🧩 Componentes extras

- **Docker Compose**: ferramenta para definir e gerenciar multi-containers com um único arquivo YAML.
- **Docker Swarm**: solução de orquestração nativa do Docker para clusters.
- **Kubernetes**: alternativa mais robusta de orquestração, amplamente usada em produção.

## 🚀 Por que usar Docker?

- Elimina o clássico problema de "funciona na minha máquina";
- Facilita testes e CI/CD;
- Reduz o tempo de setup de ambiente;
- Ideal para aplicações em microserviços;
- Suporte a orquestração com Docker Compose e Kubernetes.

## ▶️ Comandos Essenciais

### 🔹 `docker build`
Cria uma imagem a partir de um `Dockerfile`.

```bash
docker build -t minha-imagem:1.0 .
```

**Argumentos úteis:**

 * `-t`: nomeia a imagem (<`nome>:<tag>`)
 * `-f`: especifica o caminho de um `Dockerfile`
 * `--no-cache`: não usa cache no build

### 🔹 `docker run`
Cria e executa um container a partir de uma imagem.

```bash
sudo docker run -p 8080:8080 app
```

**Argumentos úteis:**

 * `-d:` modo detached (em segundo plano)
 * `-p:` mapeia porta (host:container)
 * `--name:` define um nome para o container
 * `-v:` monta volumes (host:container)
 * `--rm`: remove o container após parada
 * `-e`: define variáveis de ambiente (`-e VAR=valor`)

### 🔹 `docker ps`
Lista os containers em execução.

```bash
docker ps
```
**Argumentos úteis:**

 * `-a`: lista todos os containers (inclui parados)
 * `-q`: mostra apenas os IDs
 * `--filter`: aplica filtros (ex: `--filter status=exited`)

### 🔹 `docker images`
Lista as imagens disponíveis localmente.

```bash
docker images
```

**Argumentos úteis:**

 * `-a`: mostra todas as imagens (incluindo intermediárias)
 * `--filter`: filtra por nome, tamanho, etc.

### 🔹 `docker exec`
Executa comandos dentro de um container em execução.


```bash
docker exec -it meu-container bash
```

**Argumentos úteis:**
 * `-i`: mantém entrada interativa
 * `-t`: aloca um terminal TTY
 * `-u`: executa como usuário específico (`-u root`)

### 🔹 `Controle de containers`
Controla o estado de containers.

```bash
docker stop <name/ID>
docker start <name/ID>
docker restart <name/ID>
```

### 🔹 `docker rm`
Remove containers.

```bash
docker rm meu-container
```

**Argumentos úteis:**
 * `-f`: força a remoção (mesmo se estiver rodando)
 * `-v`: remove volumes associados

### 🔹 `docker rmi`
Remove imagens.

```bash
docker rmi minha-imagem
```

**Argumentos úteis:**

 * `-f`: força remoção da imagem
 * `--no-prune`: não remove imagens intermediárias

### 🔹 `docker pull / docker push`
 * `pull`: baixa uma imagem do Docker Hub ou registry.
 * `push`: envia uma imagem para o Docker Hub ou registry.

```bash
docker pull nginx
docker push meu-repo/minha-imagem
```

### 🔹 `docker logs`
Exibe os logs de um container.

```bash
docker logs meu-container
```

**Argumentos úteis:**

 * `-f`: follow, segue os logs em tempo real
 * `--since`: logs desde um tempo específico (ex: `--since=1h`)

### 🔹 `docker volume`
Gerencia volumes.

```bash
docker volume create meu-volume
docker volume ls
docker volume inspect meu-volume
docker volume rm meu-volume
```
### ⚙️ Outros comandos úteis
 * `docker network ls`: lista redes
 * `docker inspect`: mostra detalhes internos (JSON)
 * `docker compose`: usa o Docker Compose (`docker compose up`, `down`, `logs`, etc.)
 * `docker stats`: exibe uso de CPU, memória e rede dos containers

---

## 🌐 O que é Docker Network?
Docker Network é a camada de rede virtual que conecta os containers. Quando você cria um container, ele é automaticamente conectado a uma rede (por padrão, a rede `bridge`) mas você também pode definir redes personalizadas com diferentes comportamentos e isolamento.

<div align="center">
   <img src="https://raw.githubusercontent.com/Willian-Brito/docker-learning/refs/heads/main/prints/networking.png" height="400" />
</div>

## 🧠 Como funciona a comunicação entre containers?
 * Containers na mesma rede Docker (por exemplo, uma rede do tipo bridge ou overlay) podem se comunicar entre si pelo nome do container ou pelo nome de serviço no Docker Compose.

 * Se os containers estão em redes diferentes, a comunicação direta não é possível a menos que você as conecte manualmente.

 * A comunicação é feita via endereçamento interno DNS, gerenciado automaticamente pelo Docker.

 ## 🔌 Tipos de rede no Docker

| Tipo         | Descrição
|--------------|-----------------------------------------------------------------------------------------------|
| `brige`      | 	Rede padrão criada para containers standalone. Comunicação entre containers via IP ou nome.  |
| `host`       | 	O container compartilha a rede do host. Não há isolamento de rede                            |
| `none`       | O container não tem acesso a nenhuma rede. Totalmente isolado.                                |
| `overlay`    | Usada em ambientes com Docker Swarm. Permite comunicação entre hosts diferentes.              |
| `macvlan`    | 	Dá ao container um IP da rede física. Útil para acesso direto em redes locais.               |

## 🛠️ Comandos Docker Network úteis

### 🔍 Ver redes existentes

```bash
docker network ls
```

### 👀 Inspecionar uma rede

```bash
docker network inspect nome-da-rede
```

### ➕ Criar uma rede bridge personalizada

```bash
docker network create minha-rede
```
### 🧩 Conectar um container a uma rede

```bash
docker network connect minha-rede meu-container
```

### 🧯 Desconectar um container de uma rede

```bash
docker network disconnect minha-rede meu-container
```


## 🔒 Isolamento de rede
 * Containers em diferentes redes não conseguem se ver.
 * Você pode usar isso para segurança e controle de acesso entre microserviços.

---

## 📦 O que é o Docker Compose?
O **Docker Compose** é uma ferramenta que permite definir e gerenciar múltiplos containers Docker como parte de uma aplicação, utilizando um único arquivo de configuração (docker-compose.yml). Ele facilita a orquestração de ambientes de desenvolvimento, testes e até deploy local de aplicações complexas.

**O Docker Compose te permite:**

 - Definir vários serviços (como API, banco de dados, cache) em um único arquivo YAML.
 - Executar todos os containers de uma vez com um único comando.
 - Especificar redes, volumes, variáveis de ambiente, portas e dependências de forma declarativa.

## 🛠️ Como funciona?
 1. Você cria um arquivo`docker-compose.yml`.
 2. Define os serviços da sua aplicação: cada um com imagem, build, portas, volumes, variáveis, etc.
 3. Executa os comandos `docker compose up` ou `docker compose down` para subir ou derrubar o ambiente.

## 🔧 Principais Comandos

| Comando                                     | Descrição                                                   |
|--------------------------------------------|-------------------------------------------------------------|
| `docker compose up`                        | Inicia os containers (cria se necessário).                  |
| `docker compose up -d`                     | Inicia os containers em background (modo detached).         |
| `docker compose down`                      | Para e remove containers, redes e volumes anônimos.         |
| `docker compose ps`                        | Lista os serviços/containers em execução.                   |
| `docker compose logs`                      | Exibe os logs de todos os serviços definidos no Compose.    |
| `docker compose logs -f`                   | Exibe os logs em tempo real (modo follow).                  |
| `docker compose build`                     | Constrói ou reconstrói as imagens dos serviços.             |
| `docker compose restart`                   | Reinicia todos os serviços.                                 |
| `docker compose stop`                      | Para todos os containers sem removê-los.                    |
| `docker compose exec <serviço> <comando>`  | Executa um comando em um container em execução.             |
| `docker compose run <serviço> <comando>`   | Cria e executa um novo container temporário para o serviço. |
| `docker compose config`                    | Valida e mostra o conteúdo processado do `docker-compose.yml`. |


## ✅ Vantagens do Docker Compose
 - Produtividade: Evita ter que rodar `docker run` várias vezes manualmente.
 - Reprodutibilidade: Configuração versionada e reutilizável.
 - Isolamento: Serviços rodam em redes e volumes separados.
 - Portabilidade: Fácil de usar em times ou CI/CD com `docker compose`.

## 🔁 Docker Compose x Kubernetes
 - O Compose é ideal para ambientes de desenvolvimento e testes locais.
 - Kubernetes é mais robusto para produção em larga escala, mas mais complexo.
 - O Compose pode gerar arquivos para Kubernetes (`docker compose convert` com Docker Desktop).

---
## 📂 Tipos de volumes no Docker

No Docker, existem diferentes tipos de volumes que podem ser usados para persistir dados ou compartilhar arquivos entre o host e os contêineres.

<div align="center">
   <img src="https://raw.githubusercontent.com/Willian-Brito/docker-learning/refs/heads/main/prints/volumes.png" height="400" />
</div>

### 📑 Tabela Comparativa

| Tipo         | Comando (exemplo)                       | Descrição |
|--------------|------------------------------------------|-----------|
| **Volume**   | `-v meu_volume:/app/data`               | Gerenciado pelo Docker. Ideal para persistência de dados. |
| **Bind mount** | `-v /caminho/no/host:/app/data`       | Usa um caminho específico do sistema de arquivos do host. |
| **tmpfs**    | `--tmpfs /app/tmp`                      | Armazena dados apenas na RAM. Volátil e rápido. |

### 📦 1. Volume

- Criado e gerenciado pelo Docker com `docker volume create`.
- Armazenado geralmente em `/var/lib/docker/volumes`.
- Ideal para persistência de dados entre reinícios de containers.

**Exemplo:**:

```bash
docker run -v meu_volume:/app/data my_image
docker run --name destino -it --mount type=volume,source=meu_volume,target=/app ubuntu bash
```

### 📎 2. Bind Mount

- Usa um caminho real do host.
- Muito útil durante o desenvolvimento, pois permite editar os arquivos localmente.
- Atenção: pode ser inseguro se não bem controlado em produção.

**Exemplo:**
```bash
docker run -v /home/usuario/projeto:/app my_image
docker run -it --mount type=bind,source=/home/h1s0k4/demo_bind_mount,target=/data ubuntu bash
```
### ⚡ 3. tmpfs

- Armazena os dados diretamente na memória RAM.
- Os dados são voláteis (desaparecem ao reiniciar ou parar o contêiner).
- Excelente para dados temporários ou sensíveis.

**Exemplo:**
```bash
docker run --tmpfs /app/tmp my_image
docker run --name origem-temp -it --mount type=tmpfs,destination=/mytmp ubuntu bash
```

### 🧠 Quando usar cada um?

| Caso de uso                           | Tipo recomendado |
| ------------------------------------- | ---------------- |
| Persistência de dados                 | Volume           |
| Compartilhamento com arquivos do host | Bind Mount       |
| Dados temporários ou sensíveis        | tmpfs            |

---

## 🖼️ Imagens Docker Multiplataforma

Uma imagem Docker multiplataforma é uma imagem que pode ser executada em diferentes arquiteturas de CPU e sistemas operacionais, como:

- amd64 (arquitetura x86_64, comum em desktops e servidores)
- arm64 (usada em dispositivos como Raspberry Pi, Apple M1/M2, etc.)
- arm/v7, ppc64le, s390x, entre outras

Essas imagens são construídas de forma que o Docker escolha automaticamente a variante correta para a máquina onde está sendo executada.

### 📦 Como isso funciona?
Docker usa um recurso chamado manifest list ou multi-arch manifest, que é um "catálogo" apontando para diferentes builds da imagem, cada um compatível com uma arquitetura.

**Quando você faz:**
```bash
docker pull nginx
```
O Docker detecta sua arquitetura e baixa a versão correta automaticamente (por exemplo, `linux/amd64` ou `linux/arm64`).

### 🛠️ Como criar uma imagem multiplataforma?
Você pode usar o Buildx, uma ferramenta avançada do Docker CLI:

**1. Ative o Buildx**
```bash
docker buildx create --use
docker buildx create --name meu-builder --use --platform linux/amd64,linux/arm64 # Escolhendo as plataformas
```

**2. Iniciar e baixar imagem `moby/buildkit` para simular outras arquiteturas de processadores**
```bash
docker buildx inspect --bootstrap meu-builder
```

**3. Faça login no Docker Hub (ou outro registry)**
```bash
docker login
```

**4. Construa e publique a imagem multiplataforma:**
```bash
docker buildx build --platform linux/amd64,linux/arm64 -t seu_usuario/imagem:tag --push .
docker buildx build --platform linux/amd64,linux/arm64 -t willianbrito00/angular-multi:latest --push .
```
> 🔁 Use `--push` para enviar diretamente ao Docker Hub (ou registry escolhido).

> ✅ O `--platform` define as arquiteturas que você quer suportar.

### 💡 Por que usar imagens multiplataforma?

| Vantagem                           | Explicação                                                     |
| ---------------------------------- | -------------------------------------------------------------- |
| **Portabilidade**                  | Uma única imagem atende várias arquiteturas                    |
| **Compatibilidade com IoT e edge** | Suporte nativo para ARM (Raspberry, Apple M1/M2 etc)           |
| **Redução de manutenção**          | Um repositório para múltiplas arquiteturas                     |
| **Distribuição mais flexível**     | Usuários não precisam se preocupar com a arquitetura ao baixar |


---

## ☸️ Kubernetes
**Kubernetes** (também chamado de **K8s**) é uma **plataforma open source** para **orquestração de contêineres**. Ele foi originalmente desenvolvido pelo **Google** e hoje é mantido pela **Cloud Native Computing Foundation (CNCF)**.

Ele ajuda a **implantar**, **escalar** e **gerenciar aplicações em contêineres** (como os criados com Docker) de forma automática e eficiente.

<div align="center">
   <img src="https://raw.githubusercontent.com/Willian-Brito/docker-learning/refs/heads/main/prints/kubernetes-2.png" height="400" />
</div>

### 🔧 O que o Kubernetes faz?
 1. **Orquestra contêineres:** decide onde e como os contêineres devem rodar.
 2. **Gerencia o ciclo de vida:** reinicia contêineres que falham, substitui instâncias e controla atualizações.
 3. **Escalabilidade automática:** aumenta ou reduz a quantidade de réplicas da aplicação conforme a carga.
 4. **Distribuição de carga:** balanceia o tráfego entre os contêineres.
 5. **Descoberta de serviços:** contêineres podem se comunicar sem saber IPs fixos.
 6. **Auto-healing:** substitui ou reinicia contêineres com problemas automaticamente.
 
### 📦 Conceitos principais

| Conceito       | Descrição                                                                 |
|----------------|---------------------------------------------------------------------------|
| **Pod**        | Unidade mínima no Kubernetes. Pode conter um ou mais contêineres.         |
| **Node**       | Um servidor (físico ou virtual) que roda os Pods.                         |
| **Cluster**    | Conjunto de Nodes gerenciados pelo Kubernetes.                            |
| **Deployment** | Controla a criação e atualização de Pods.                                 |
| **Service**    | Define como os Pods são acessados na rede (internamente ou externamente). |
| **ConfigMap**  | Armazena configurações não sensíveis que podem ser usadas pelos Pods.     |
| **Secret**     | Armazena dados sensíveis como senhas e tokens de forma segura.            |
| **Ingress**    | Gerencia o tráfego HTTP externo para serviços internos.                   |

### 🚀 Benefícios
 - Alta disponibilidade
 - Escalabilidade horizontal
 - Infraestrutura declarativa (infra como código)
 - Portabilidade entre nuvem e on-premises
 - Automatização de tarefas complexas

### 🔌 Onde o Kubernetes é usado?
 - Hospedagem de microserviços
 - Plataformas SaaS
 - CI/CD pipelines
 - Aplicações que exigem alta disponibilidade e escalabilidade