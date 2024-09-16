# LeadTech - Estilista Inteligente: Virtual Try-On (VTON)

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

