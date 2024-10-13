# qual imagem eu quero rodar

FROM jupyter/scipy-notebook

# criar e definir o diretório de trabalho

WORKDIR /home/jovyan/work

# copiar todos arquivos do projeto para dentro do container

COPY . /home/jovyan/work

#Expor a porta para o Jupyter NOtebook

EXPOSE 8888


# Comando para iniciar e rodar o Jupyter Notebook

CMD ["jupyter", "notebook", "--ip=0.0.0.0", "--port=8888", "--no-browser", "--allow-root"]
