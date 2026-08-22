# Projeto Dígitos Lotofácil
Este projeto utiliza um DataSet de dígitos de bilhetes da Lotofácil para treinamento e inferência de modelos de IA.
Os dígitos compreendem os números de 01 a 25, digitalizados e tratados para incluir ruídos diversos nas imagens para aperfeiçoar o treinamento.

Em seguida o treinamento gerou os pesos que foram utilizados num projeto JavaScript rodando localmente num navegador bastando para isso rodar um servidor Python.

Para testar as inferências pode-se usar os modelos de testes do próprio Dataset que contem novas imagens de dígitos com mais ruídos.

Kaggle(dataset): https://www.kaggle.com/datasets/devapanheidoexcel/digits-lotofacil-bilhete

Vídeo demonstração rápida: https://youtu.be/nU86au4l-0k

## Sobre o projeto
Aqui você encontra um projeto que utiliza um modelo de IA treinado especificamente para reconhecer os dígitos dos bilhetes da Lotofácil utilizados nos jogos.

A proposta inicial é identificar estes dígitos individualmente, para numa evolução reconher todos os dígitos que estiverem em um bilhete.

O projeto contém as seguintes partes:

- **dataset-30x10x10.zip**: arquivo que deve ser descomprimido localmente contendo todas as imagens utilizadas para o treinamento da IA e para testes do modelo. Descompacte este arquivo e verá as pastas "train" (treinamento), "val" (validação do treinamento) e "test" (testes do modelo).
Estas imagens foram escaneadas de bilhetes e tratadas para acrescentar diversos tipos de "ruídos" garantindo variações reais, como números um pouco apagados, riscados, desalinhados e afins.

- **tm-my-image-model**: pasta contendo os metadados do modelo e os pesos gerados pelo treinamento.

- **script_numbers_lotofacil_pick_image.html**: interface gráfica com código em JavaScript contendo o script para realizar a inferência usando o modelo. Utilizamos o TensorFlow.js para carregar os pesos do modelo e realizar a inferência. O mesmo já é carregado na inicialização.


### Rodando o projeto
A melhor maneira de se rodar este projeto é inicializando um servidor Python localmente dentro da pasta do projeto.

1. Acesse via terminal a pasta do projeto.


```bash
cd "...pastaDoProjeto"
python -m http.server 8000
# Then open http://localhost:8000/script_numbers_lotofacil_pick_image.html
```

2. Acesse o arquivo html do script a partir da barra do navegador. NÃO abra o arquivo com 2 cliques como se fosse visualizar o mesmo. 
3. Digite no navegador: http://localhost:8000/script_numbers_lotofacil_pick_image.html

4. Na tela que irá aparecer no navegador, clique no botão: "Carregar Modelo" para os pesos serem carregados em memória.
5. Em seguida irá aparecer o botão de "Selecionar Imagem". Clique no mesmo para abrir um seletor de imagens. Busque uma imagem do **dataset-30x10x10.zip** descomprimido anteriormente. Prefira buscar imagens da pasta "val" ou "test".
6. Será exibido um os percentuais de probabilidades inferidos pelo modelo indicando o quanto ele acredita que a imagem selecionada é o número correto para cada uma das dezenas de 01 a 25. A maior probabilidade deve ser a considerada a inferida pelo modelo.

Pelos testes gerais realizados, chegamos num índice de acerto próximo de **78%**. Considerando que a quantidade de imagens de treinamento geradas não foi tão grande, porém as variações de ruídos foram muitas, esse resultado é extremamente satisfatório.

Caso fossem geradas mais imagens de treinamento esse número pode subir para bem próximo dos 90% ou até mais.

### Propostas evolutivas
1. Gerar mais imagens para treinamento com vários ruídos diferentes.
2. Identificar a dezenas através do uso de uma camera. Hoje o projeto já consegue "ler" a imagem da camera conectada no PC através do script **"script_numbers_lotofacil_webcam.html"**.
3. Identificar mais de uma dezena através de uma MATRIZ onde cada dezena esteja espaçada de forma igual entre si.
4. Identificar as dezenas a partir de uma imagem real do bilhete da Lotofácil. Aqui entram algumas questões: os jogos padrões possuem 15 dezenas, porém existem bilhetes com mais de 15 dezenas. Em um bilhete pode haver até 03 jogos, ou seja, temos que identificar as dezenas de cada jogo individualmente por jogo.


