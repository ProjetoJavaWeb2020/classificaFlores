# Classificador de flores usando Inception v3 da plataforma TensorFlow


## Comandos a serem executados passo-a-passo

### Testa a instalação do Docker
docker run hello-world

### Baixa a imagem do TensorFlow
docker pull tensorflow/tensorflow

### Carregando o container TensorFlow
docker run -it --volume ${PWD}:/tf_files --workdir /tf_files --publish 6006:6006 tensorflow/tensorflow:1.1.0 bash

### Baixa arquivo retrain.py
curl -O https://raw.githubusercontent.com/tensorflow/tensorflow/r1.1/tensorflow/examples/image_retraining/retrain.py

### Baixa arquivo label_image.py
curl -L https://goo.gl/3lTKZs > label_image.py

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
python label_image.py tulipa.jpg
