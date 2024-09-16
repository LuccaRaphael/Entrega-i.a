# **LeadTech - Estilista Inteligente: Projeto de Recomendações Personalizadas e Virtual Try-On**

## **Objetivo do Projeto**
O objetivo principal do projeto **LeadTech - Estilista Inteligente** é oferecer **recomendações personalizadas** de moda e permitir que os clientes **experimentem virtualmente** as roupas, aumentando as vendas de lojas e auxiliando os clientes na tomada de decisões de compra. O projeto foi dividido em duas partes complementares:

1. **Parte 1 - Sistema de Recomendações Personalizadas**: Este sistema utiliza visão computacional para identificar itens de moda e fornecer sugestões baseadas em similaridade visual, facilitando a busca por produtos que correspondam às preferências dos clientes.
   
2. **Parte 2 - Virtual Try-On (VTON)**: Um protótipo de experimentação virtual que permite que os usuários façam upload de suas fotos e experimentem virtualmente roupas, criando uma experiência mais interativa e envolvente.

Abaixo estão as documentações detalhadas de cada parte do projeto.

**Link do Vídeo :** [Aqui](https://www.youtube.com/watch?v=6UDhFYrq2KI)

---

## **Parte 1: LeadTech - Estilista Inteligente: Sistema de Recomendações Personalizadas**

## **Objetivo Principal**
Desenvolver um **Sistema de Recomendação Personalizada** baseado em **Computer Vision**, que auxilie os clientes a encontrar produtos de moda de acordo com suas preferências e os produtos disponíveis na loja, aumentando assim as vendas ao oferecer recomendações específicas e direcionadas.

## **Objetivos Específicos**
- **Demonstração do protótipo funcional**: Apresentar o estado atual do sistema, demonstrando as funcionalidades implementadas, como detecção de itens de moda e sistema de recomendação baseado em similaridade visual.
- **Detalhamento da arquitetura de IA**: Explicar a arquitetura utilizada para detecção de objetos e embeddings de imagens, justificando a escolha dos modelos e técnicas aplicadas.
- **Base de dados utilizada**: Detalhar os datasets usados no treinamento e teste do modelo, com links e descrições sobre como os dados foram preparados.

---

## **1. Demonstração do Protótipo Funcional**

O sistema de **Recomendações Personalizadas** permite que os usuários recebam sugestões de produtos similares baseadas em imagens. A interface oferece um mecanismo de busca visual para identificar produtos similares aos itens de interesse do cliente, ajudando na tomada de decisão de compra.

O protótipo conta com as seguintes funcionalidades:
- **Detecção de Objetos de Moda**: Utilizando o modelo **YOLOv5**, o sistema detecta e recorta itens de moda em uma imagem fornecida pelo usuário.
- **Embeddings de Imagem**: A partir dos objetos detectados, o sistema gera embeddings, que são representações vetoriais das características visuais dos itens. Esses embeddings são usados para encontrar produtos visualmente semelhantes no catálogo da loja.
- **Recomendações Personalizadas**: Com base nas preferências do cliente e nos itens disponíveis na loja, o sistema sugere produtos similares, ajudando o cliente a encontrar peças que correspondam ao seu gosto.
- **Apresentação via Streamlit**: O protótipo é apresentado usando **Streamlit**, que permite que os usuários façam upload de imagens e recebam recomendações visuais em tempo real.

### **Tecnologias Utilizadas**
- **Python**: Linguagem principal para o desenvolvimento.
- **YOLOv5**: Usado para detecção de objetos de moda em imagens.
- **AutoEncoder**: Rede neural utilizada para gerar embeddings visuais dos itens detectados.
- **Streamlit**: Utilizado para criar a interface de demonstração.

## **2. Detalhamento da Arquitetura de IA**

A arquitetura do sistema de recomendações personalizadas foi desenvolvida em três fases interdependentes: **coleta e preparação de dados**, **modelagem de machine learning** e **fase de inferência**. Cada uma dessas fases desempenha um papel crucial no funcionamento do sistema, desde a coleta de dados até a recomendação final ao usuário, baseada em similaridade visual.

### **2.1 Coleta e Preparação dos Dados**
A primeira fase envolve a **coleta de dados** e sua **preparação** para treinar os modelos de detecção de objetos e de embeddings. Utilizamos datasets públicos com imagens de moda, sendo o principal deles o **Complete the Look Dataset**, que contém mais de **12.000 imagens de estilo** com caixas delimitadoras. Essas imagens são usadas para identificar e categorizar itens de moda, como roupas e acessórios.

#### **Etapas do processo:**
- **Limpeza e Transformação**: Os dados brutos coletados foram organizados utilizando a biblioteca **Pandas**, onde foram extraídas as colunas relevantes e removidos valores nulos ou strings vazias. Isso garante que o modelo seja treinado com dados consistentes e de alta qualidade.
- **Balanceamento de Classes**: Como em muitos datasets, havia uma desproporção entre as diferentes categorias de moda. Para garantir que o modelo não tenha viés em favor de certas categorias, aplicamos técnicas de balanceamento, resultando em um conjunto equilibrado de **15.657 objetos** distribuídos em **9.235 imagens**, com cerca de **1.000 imagens por categoria de moda**.
- **Correção de Imagens Corrompidas**: Utilizamos um script com **ImageMagick** para verificar e corrigir imagens corrompidas, evitando que o treinamento falhe ou sofra com entradas inválidas.
- **Criação dos Arquivos de Anotação**: Cada imagem recebeu um arquivo `.txt` associado, contendo as coordenadas de suas caixas delimitadoras e a classe dos objetos identificados. Esses arquivos são essenciais para treinar o modelo de detecção de objetos.

### **2.2 Modelo de Detecção de Objetos**
Com os dados preparados, a próxima fase é a construção e treinamento do **modelo de detecção de objetos**, responsável por identificar peças de moda em imagens. Utilizamos o **YOLOv5** pré-treinado, ajustado especificamente para detecção de roupas e acessórios.

#### **Funcionamento**:
- **Treinamento**: O modelo YOLOv5 foi ajustado com os dados anotados da fase anterior. Ele aprende a detectar objetos de moda em diferentes cenários e posições, gerando caixas delimitadoras que identificam e segmentam os itens nas imagens.
- **Resultados**: Após o treinamento, o modelo apresentou os seguintes resultados:
  - **Precisão (Precision)**: 54.8
  - **Recall**: 64.8
  - **mAP** (Mean Average Precision): 60.9

Esses resultados indicam que o modelo consegue detectar objetos com uma boa taxa de acerto, equilibrando precisão e recall.

### **2.3 Modelo de Embeddings**
Após a detecção dos objetos de moda, cada item é transformado em uma **representação vetorial** (embedding) por meio de um **AutoEncoder**. Esta representação captura as características visuais dos itens, como cor, textura e forma, permitindo que o sistema compare visualmente diferentes peças de moda.

#### **Funcionamento**:
- **Arquitetura do AutoEncoder**: O modelo de AutoEncoder é composto por um **encoder**, que comprime a imagem do item detectado em um vetor de 512 dimensões (embedding), e um **decoder**, que reconstrói a imagem a partir desse vetor.
- **Embedding de 512 Dimensões**: O "bottleneck" do AutoEncoder, onde ocorre a compressão, é o ponto onde a imagem é convertida em uma **representação vetorial** de 512 dimensões. Essa compactação permite uma busca eficiente de itens semelhantes com base em suas características visuais.
- **Comparação Visual**: Os embeddings gerados são utilizados para calcular a similaridade entre diferentes peças. Quanto mais próximo o vetor de um produto estiver de outro, mais semelhante ele é visualmente.

#### **Resultados do Modelo de Embeddings**:
- **Baseline (4096-d)**: Índice de tamanho 163.8 MB, mAP de 0.44.
- **+Layer (512-d)**: Índice de tamanho 25 MB, mAP de 0.53 (modelo utilizado no sistema).

A escolha pelo embedding de 512 dimensões foi feita para garantir um equilíbrio entre **precisão** e **eficiência computacional**, já que a redução no tamanho do vetor diminuiu o tempo de inferência e o espaço de armazenamento sem sacrificar significativamente a precisão.

### **2.4 Fase de Inferência e Recomendações**
Na fase final, o sistema já treinado utiliza os embeddings gerados para fornecer **recomendações personalizadas**. Quando o usuário faz upload de uma imagem, o modelo de detecção de objetos (YOLOv5) identifica as peças de moda na imagem e, em seguida, o modelo de embeddings compara essas peças com o catálogo da loja.

#### **Processo de Inferência**:
1. **Detecção do Item**: O YOLOv5 detecta e segmenta a peça de vestuário ou acessório.
2. **Geração do Embedding**: O AutoEncoder transforma o item detectado em um vetor de 512 dimensões.
3. **Busca por Similaridade**: O vetor gerado é comparado com os vetores já armazenados no sistema, e os itens mais semelhantes visualmente são retornados como sugestões.
4. **Apresentação ao Usuário**: As recomendações são apresentadas via interface **Streamlit**, permitindo uma navegação rápida e intuitiva.

#### **Justificativa da Arquitetura**:
A arquitetura foi desenhada para balancear **precisão** e **eficiência**. O uso do YOLOv5 garante detecção rápida e precisa, enquanto o AutoEncoder reduz a complexidade computacional na busca por similaridade, mantendo a alta precisão de recomendações.


## **3. Base de Dados Utilizada**

### **3.1 Complete the Look Dataset**
- **Descrição**: O dataset utilizado contém imagens de moda com caixas delimitadoras, fornecendo anotações detalhadas de objetos como roupas e acessórios.
- **Justificativa**: Este dataset foi escolhido pela sua riqueza em exemplos de moda variados, facilitando o treinamento de modelos de detecção e embeddings com alta precisão.
- **Link**: https://github.com/eileenforwhat/complete-the-look-dataset

---
---
---

## **Parte 2: LeadTech - Estilista Inteligente: Virtual Try-On (VTON)**

## **Objetivo Principal**
Desenvolver e apresentar um **protótipo funcional** de um sistema de **Virtual Try-On (VTON)**, que utiliza técnicas avançadas de Inteligência Artificial para permitir que os usuários experimentem roupas virtualmente. Além disso, fornecer uma **análise detalhada da arquitetura de IA** utilizada no projeto.

## **Objetivos Específicos**
- **Demonstração do protótipo funcional**: Apresentar o estado atual do projeto, destacando as funcionalidades implementadas até o momento, como segmentação de roupas, estimativa de pose e composição de imagens.
- **Detalhamento da arquitetura de IA**: Descrever a arquitetura utilizada, justificando a escolha das tecnologias, ferramentas e algoritmos empregados, além de explicar o processo de implementação.
- **Base de dados utilizada**: Apresentar e justificar a escolha dos datasets utilizados para treinamento e teste do sistema.

---

## **1. Demonstração do Protótipo Funcional**

O sistema de **Virtual Try-On** foi desenvolvido para permitir que os usuários façam upload de suas fotos e experimentem diferentes peças de vestuário virtualmente. A versão atual do protótipo implementa as seguintes funcionalidades principais:

- **Segmentação de Roupas**: Utilizando um modelo pré-treinado, o sistema isola a peça de vestuário da imagem de entrada. Essa etapa é fundamental para garantir que a roupa seja adequadamente separada do plano de fundo.
- **Estimativa de Pose**: Através do **PoseNet**, o sistema identifica os principais pontos do corpo humano, como ombros, cotovelos, quadris e joelhos. Esses pontos são usados para alinhar a roupa corretamente à pessoa.
- **Composição de Imagens**: Com base na estimativa de pose e na segmentação da roupa, o sistema ajusta a peça à pose da pessoa, criando uma composição de imagem realista.
- **Apresentação via Streamlit**: O protótipo é apresentado através da interface interativa criada com **Streamlit**, que permite o upload de imagens pelos usuários e a visualização dos resultados de forma simples e intuitiva.

### **Tecnologias Utilizadas**
- **Python**: Linguagem principal para desenvolvimento.
- **TensorFlow e OpenCV**: Usados para a implementação de modelos de segmentação e pose.
- **Streamlit**: Para criar a interface de demonstração e facilitar o upload de imagens e a visualização do resultado final.

---

## **2. Detalhamento da Arquitetura de IA**

A arquitetura de IA foi escolhida com o objetivo de oferecer alta precisão na **segmentação de roupas** e na **estimativa de pose**, permitindo que o ajuste da peça ao corpo seja o mais natural possível.

### **2.1 Segmentação de Roupas**
Utilizamos um modelo pré-treinado baseado em redes convolucionais, ajustado para tarefas de segmentação de imagens. Os modelos foram treinados com o **VITON HR Dataset** e o **iMaterialist Fashion Dataset**, que fornecem uma grande quantidade de imagens de alta qualidade de pessoas vestindo diferentes tipos de roupas. 

- **Ferramenta Utilizada**: O módulo de **Cloths Segmentation** foi implementado para gerar máscaras binárias, que separam as roupas do restante da imagem.
- **Processo**: O sistema aplica essa máscara para extrair apenas a peça de vestuário, removendo o fundo.

### **2.2 Estimativa de Pose**
A estimativa de pose é realizada pelo **PoseNet**, um modelo de rede neural leve que detecta pontos-chave do corpo humano. Esses pontos são cruciais para o ajuste da roupa.

- **Tecnologia**: Implementado com **TensorFlow** e integrado ao pipeline de processamento da imagem com **OpenCV**.
- **Justificativa**: O PoseNet foi escolhido pela sua eficiência e precisão em detectar pontos-chave do corpo em várias poses, garantindo que a roupa seja ajustada corretamente.

### **2.3 Composição de Imagens**
O sistema finaliza o processo ajustando a roupa à pose da pessoa e gera a imagem composta. Isso é feito por um script Python (**main.py**), que garante que o vestuário seja posicionado de forma natural no corpo, levando em consideração o tamanho e a posição dos pontos-chave detectados.

### **Por que essa arquitetura foi escolhida?**
A combinação de **redes convolucionais para segmentação** e **PoseNet para detecção de pontos-chave** foi escolhida pela sua robustez e eficiência. Além disso, a vasta quantidade de dados disponível nos datasets utilizados garantiu um bom desempenho em diferentes tipos de imagens, mantendo a precisão tanto na segmentação quanto na composição final.

---

## **3. Base de Dados Utilizada**

### **3.1 VITON HR Dataset**
- **Descrição**: O VITON HR Dataset contém uma grande coleção de imagens de pessoas e roupas, usadas principalmente em projetos de Virtual Try-On.
- **Justificativa**: Este dataset foi utilizado pela sua ampla variedade de vestuário e qualidade de imagens, permitindo uma segmentação mais precisa. 
- **Link**: https://drive.google.com/drive/folders/0B8kXrnobEVh9fnJHX3lCZzEtd20yUVAtTk5HdWk2OVV0RGl6YXc0NWhMOTlvb1FKX3Z1OUk?resourcekey=0-OIXHrDwCX8ChjypUbJo4fQ

### **3.2 iMaterialist Fashion Dataset**
- **Descrição**: O iMaterialist é um dataset especializado em imagens de moda, categorizado em diferentes tipos de vestuário, o que facilita o treinamento de redes para segmentação.
- **Justificativa**: Sua diversidade e riqueza de informações permitiram que o sistema reconhecesse e segmentasse diferentes tipos de roupas com alta precisão.
- **Link**: https://www.kaggle.com/c/imaterialist-fashion-2019-FGVC6















































