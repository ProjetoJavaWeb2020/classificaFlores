# Classificador de flores usando Inception v3 da plataforma TensorFlow

### ***Devido o tamanho do diretório onde contêm os arquivos necessários para executar os procedimentos abaixo ser maior que 100MB o mesmo foi carregado no Google Drive***
>> https://drive.google.com/drive/folders/1E4LIKSvx0Mo5lwWm8Nk_TpVKX8Rlayih?usp=sharing


## Passo-a-passo com treino e classificação

### Baixe o Docker
https://www.docker.com/get-started

### Abrir PowerShell
Crie uma pasta no computador, pressione o shift + clique com botão direito "Abrir janela PowerShell aqui" 

### Testa a instalação do Docker
docker run hello-world

### Baixa a imagem do TensorFlow
docker pull tensorflow/tensorflow

### Carregando o container TensorFlow
docker run -it --volume ${PWD}:/tf_files --workdir /tf_files --publish 6006:6006 tensorflow/tensorflow:1.1.0 bash

### Adicionar os seguintes arquivos no diretório criado
  
>> Crie uma pasta com nome flores e adicione dentro dela as pastas de imagens "margarida" e "tulipa" que estão no repositório.
>> Caso queira treinar outras categorias de flores basta colocar as pastas com as imagens das categorias desejadas.
>> Banco de imagens disponível : http://download.tensorflow.org/example_images/flower_photos.tgz
   
>> Baixa arquivo retrain.py

>> curl -O https://raw.githubusercontent.com/tensorflow/tensorflow/r1.1/tensorflow/examples/image_retraining/retrain.py

>> Baixa arquivo label_image.py

>> curl -L https://goo.gl/3lTKZs > label_image.py

### Baixa o Inception e começa o treinamento
python -m retrain \
  --bottleneck_dir=bottlenecks \
  --how_many_training_steps=500 \
  --model_dir=models/ \
  --summaries_dir=training_summaries/"${ARCHITECTURE}" \
  --output_graph=retrained_graph.pb \
  --output_labels=retrained_labels.txt \
  --architecture="${ARCHITECTURE}" \
  --image_dir=flores

### Testa o modelo treinado
>> Baixe imagens de acordo com a categoria treinada, margarida ou tulipa, o coloque no diretório onde estão todos os arquivos
>> Use o comando abaixo passando o nome da imagem baixada

>> python label_image.py tulipa.jpg

## Passo-a-passo para somente classificar as flores

### Baixe o Docker
https://www.docker.com/get-started

### Abrir PowerShell
Crie uma pasta no computador, pressione o shift + clique com botão direito "Abrir janela PowerShell aqui" 

### Testa a instalação do Docker
docker run hello-world

### Baixa a imagem do TensorFlow ( se não já estiver baixado )
docker pull tensorflow/tensorflow

### Baixe os arquivos disponíveis
baixe os arquivos deste repositório e coloque na pasta criada

### Carregando o container TensorFlow
docker run -it --volume ${PWD}:/tf_files --workdir /tf_files --publish 6006:6006 tensorflow/tensorflow:1.1.0 bash

### Testa o modelo treinado
python label_image.py tulipa.jpg


