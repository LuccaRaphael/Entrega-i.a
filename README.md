# **LeadTech - Estilista Inteligente: Projeto de Recomendações Personalizadas e Virtual Try-On**

## **Objetivo do Projeto**
O objetivo principal do projeto **LeadTech - Estilista Inteligente** é oferecer **recomendações personalizadas** de moda e permitir que os clientes **experimentem virtualmente** as roupas, aumentando as vendas de lojas e auxiliando os clientes na tomada de decisões de compra. O projeto foi dividido em duas partes complementares:

1. **Parte 1 - Sistema de Recomendações Personalizadas**: Este sistema utiliza visão computacional para identificar itens de moda e fornecer sugestões baseadas em similaridade visual, facilitando a busca por produtos que correspondam às preferências dos clientes.
   
2. **Parte 2 - Virtual Try-On (VTON)**: Um protótipo de experimentação virtual que permite que os usuários façam upload de suas fotos e experimentem virtualmente roupas, criando uma experiência mais interativa e envolvente.

Abaixo estão as documentações detalhadas de cada parte do projeto.

**Link do Vídeo do Protótipo:** [Aqui](https://smartstylist.streamlit.app)

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

---

## **2. Detalhamento da Arquitetura de IA**

A arquitetura foi desenvolvida em três fases: **coleta de dados**, **modelagem de machine learning** e **fase de inferência**, onde o sistema serve as recomendações com base em similaridade visual.

### **2.1 Coleta e Preparação dos Dados**
Para treinar o modelo de detecção de objetos e o modelo de embeddings, foram utilizados datasets públicos contendo imagens de moda. O dataset principal foi retirado do paper "Complete the Look Dataset" e inclui mais de **12.000 imagens de estilo** com caixas delimitadoras, usadas para identificar objetos de moda.

Os passos para preparação dos dados foram:
- **Limpeza e Transformação**: Os dados foram organizados utilizando **Pandas**, extraindo as colunas relevantes e removendo strings vazias.
- **Balanceamento de Classes**: O dataset foi equilibrado, com 1.000 imagens por categoria de moda, resultando em um total de **15.657 objetos e 9.235 imagens**.
- **Correção de Imagens Corrompidas**: Um script do **ImageMagick** foi utilizado para corrigir imagens corrompidas.
- **Criação dos Arquivos de Treinamento**: Cada imagem recebeu um arquivo `.txt` contendo as coordenadas e classes dos objetos para treinamento do modelo de detecção.

### **2.2 Modelo de Detecção de Objetos**
Para detectar os itens de moda nas imagens, foi utilizado o modelo **YOLOv5** pré-treinado, ajustado para identificar roupas e acessórios em imagens de moda. O resultado foi:
- **Precisão (Precision)**: 54.8
- **Recall**: 64.8
- **mAP** (Mean Average Precision): 60.9

### **2.3 Modelo de Embeddings**
O modelo de embeddings utiliza uma arquitetura de **AutoEncoder** para transformar as imagens dos itens detectados em representações vetoriais. O encoder e decoder foram construídos com **camadas convolucionais** para capturar as características visuais. O vetor gerado no "bottleneck" do AutoEncoder é um **embedding de 512 dimensões**, que serve como base para a recomendação.

Os resultados do modelo de embeddings foram:
- **Baseline (4096-d)**: Tamanho do índice 163.8 MB, mAP de 0.44
- **+Layer (512-d)**: Tamanho do índice 25 MB, mAP de 0.53 (Modelo utilizado no sistema).

### **Justificativa da Escolha dos Modelos**
A escolha do **YOLOv5** foi baseada na sua capacidade de detecção eficiente em tempo real, enquanto o **AutoEncoder** com embeddings de 512 dimensões foi selecionado pela sua capacidade de representar visualmente os itens com alta precisão, mantendo a eficiência computacional.

---

## **3. Base de Dados Utilizada**

### **3.1 Complete the Look Dataset**
- **Descrição**: O dataset utilizado contém imagens de moda com caixas delimitadoras, fornecendo anotações detalhadas de objetos como roupas e acessórios.
- **Justificativa**: Este dataset foi escolhido pela sua riqueza em exemplos de moda variados, facilitando o treinamento de modelos de detecção e embeddings com alta precisão.
- **Link**: https://github.com/eileenforwhat/complete-the-look-dataset

  

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















































