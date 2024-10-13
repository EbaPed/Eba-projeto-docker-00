# Projeto com Docker

### **1. Rodando o Projeto sem `docker-compose`**

#### Passo 1: Criar a Estrutura do Projeto

Primeiro, crie a estrutura de pastas e os arquivos necessários para o seu projeto.

```bash
mkdir meu-projeto-docker
cd meu-projeto-docker
```

#### Passo 2: Criar o Dockerfile

Adicione o seguinte conteúdo ao seu `Dockerfile`:

```Dockerfile
# Usar a imagem base do Jupyter SciPy Notebook
FROM jupyter/scipy-notebook


# Definir o diretório de trabalho no contêiner como o diretório padrão do Jupyter
WORKDIR /home/jovyan/work

# Copiar todos os arquivos do projeto para o contêiner
COPY . /home/jovyan/work

# Expor a porta padrão do Jupyter Notebook
EXPOSE 8888

# Comando para iniciar e rodar o Jupyter Notebook
CMD ["jupyter", "notebook", "--ip=0.0.0.0", "--port=8888", "--no-browser", "--allow-root"]
```

#### Passo 3: Construir a Imagem

Construa a imagem Docker usando o seguinte comando no diretório do projeto:

```bash
docker build -t meu-projeto-docker .
```

#### Passo 4: Rodar o Contêiner

Inicie o contêiner com a seguinte linha de comando:

```bash
docker run -p 8888:8888 meu-projeto-docker
```

### Acessando o Jupyter Notebook

Após executar o comando acima, você poderá acessar o Jupyter Notebook no seu navegador em:

```
http://localhost:8888
```

---

### 2. **Rodando o Projeto com `docker-compose`**

#### Passo 1: Criar a Estrutura do Projeto

A estrutura do projeto deve ser semelhante à seguinte:

```bash
mkdir meu-projeto-docker-compose
cd meu-projeto-docker-compose
```

#### Passo 2: Criar o Dockerfile

Adicione o seguinte conteúdo ao seu `Dockerfile`:

```Dockerfile
# Usar a imagem base do Jupyter SciPy Notebook
FROM jupyter/scipy-notebook

# Definir o diretório de trabalho no contêiner como o diretório padrão do Jupyter
WORKDIR /home/jovyan/work

# Copiar todos os arquivos do projeto para o contêiner
COPY . /home/jovyan/work

# Expor a porta padrão do Jupyter Notebook
EXPOSE 8888

# Comando para iniciar e rodar o Jupyter Notebook
CMD ["jupyter", "notebook", "--ip=0.0.0.0", "--port=8888", "--no-browser", "--allow-root"]
```

#### Passo 3: Criar o arquivo `docker-compose.yml`

Adicione o seguinte conteúdo ao seu `docker-compose.yml`:

```yaml
version: '3'
services:
  notebook:
    build: .
    ports:
      - "8888:8888"  # Mapeia a porta 8888 do contêiner para a porta 8888 do host
    volumes:
      - .:/home/jovyan/work  # Mapeia a raiz do projeto local para o /home/jovyan no contêiner
    environment:
      - JUPYTER_ENABLE_LAB=yes  # Ativa o JupyterLab
    command: start-notebook.sh --ip=0.0.0.0 --NotebookApp.token='' --NotebookApp.password=''
```

#### Passo 4: Construir e Rodar o Contêiner

Agora, você pode construir e rodar o contêiner com um único comando:

```bash
docker-compose up --build
```

### Acessando o Jupyter Notebook

Assim como no primeiro método, você poderá acessar o Jupyter Notebook no seu navegador em:

```
http://localhost:8888
```

### Conclusão

Com estas instruções, você pode executar um projeto Python utilizando Jupyter Notebook tanto com Docker Compose quanto sem ele. O método com Docker Compose oferece uma maneira mais simples e prática de gerenciar contêineres, especialmente quando seu projeto envolve múltiplos serviços ou dependências complexas.

Testem ao máximo e pesquisem sobre a ferramenta. E já sabem, qualquer dúvida, estamos aqui para ajudá-lo!