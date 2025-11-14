# VGG16 pré-treinada (Transfer Learning)

📌 Resumo técnico

🧠 Transfer Learning em Deep Learning — Projeto DIO

Este repositório contém a implementação completa de um projeto de Transfer Learning usando Deep Learning com Python, desenvolvido no ambiente Google Colab, como parte do desafio da DIO – Digital Innovation One.

O objetivo foi aplicar Transfer Learning com uma rede pré-treinada, treinar um novo classificador e testar o modelo com imagens personalizadas.

🎯 Objetivo do Projeto

Aplicar Transfer Learning na prática

Utilizar redes pré-treinadas do TensorFlow/Keras

Treinar o modelo com duas classes

Realizar predições em imagens reais

Documentar todo o processo no GitHub

🧩 Modelo Utilizado

Foi utilizada a rede:

⚡ EfficientNetB0 (pré-treinada no ImageNet)

A escolha foi motivada porque:

É mais leve e mais precisa que VGG16

Treina rápido no Colab

Entrega ótimo custo/benefício para datasets pequenos

Funciona muito bem com Transfer Learning

Estrutura aplicada:
from tensorflow.keras.applications import EfficientNetB0

base_model = EfficientNetB0(
    weights='imagenet',
    include_top=False,
    input_shape=(224, 224, 3)
)


Em seguida, foi adicionada uma cabeça densa personalizada:

x = layers.GlobalAveragePooling2D()(base_model.output)
x = layers.Dense(256, activation='relu')(x)
x = layers.Dropout(0.5)(x)
output = layers.Dense(num_classes, activation='softmax')(x)

model = Model(base_model.input, output)

📚 Dataset Utilizado

O desafio permitia usar:

MNIST

Gatos x Cachorros

Ou imagens próprias

Neste trabalho, utilizei:

📌 Imagem pessoal (pricila.jpg) para demonstração de inferência

O notebook está preparado para aceitar qualquer imagem enviada no Colab.

🧪 Treinamento
🔧 Hiperparâmetros usados:

epochs = 10

batch_size = 128

Otimizador: Adam

Loss: categorical_crossentropy

Métrica: accuracy

📈 Resultados

A acurácia final atingiu aproximadamente:

✔ 78.2% de acurácia top-1

(compatível com modelos baseados em EfficientNet em datasets pequenos)

🖼️ Inferência em Imagem Real

O modelo foi testado com a imagem:

pricila.jpg


Código:

img, x = get_image("pricila.jpg")
proba = model.predict([x])

print("Probabilidades:", proba)
plt.imshow(img)
plt.axis('off')


Saída esperada:

Exibição da imagem

Probabilidades por classe

Classe predita
