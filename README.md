# Projeto: Virtual Try-On (VTON)

## Objetivo Principal

O objetivo principal deste projeto é o **desenvolvimento de um sistema de Virtual Try-On (VTON)** que permite aos usuários experimentarem virtualmente roupas usando uma imagem de entrada. O sistema combina técnicas avançadas de IA, como segmentação de roupas, estimativa de pose e composição de imagens, para gerar uma visualização realista da pessoa usando a roupa selecionada.

## Objetivos Específicos

### 1. Demonstração do Protótipo Funcional
Até o momento, o projeto implementa as seguintes funcionalidades:
- **Segmentação de Roupas**: Utilizando um modelo pré-treinado, o sistema é capaz de segmentar a roupa de uma imagem de entrada e gerar uma máscara que isola a peça de vestuário.
- **Estimativa de Pose**: A estimativa de pose do usuário é realizada por meio de um modelo de PoseNet, que detecta os principais pontos do corpo e permite alinhar a roupa com a pessoa.
- **Processamento de Imagens**: As imagens são processadas para remover o fundo e ajustar a roupa à pose da pessoa, criando uma composição final onde a pessoa aparece vestindo a roupa virtualmente.

### 2. Detalhamento da Arquitetura de IA

#### Segmentação de Roupas
A segmentação de roupas é realizada pelo script `get_cloth_mask.py`, que usa um modelo pré-treinado para gerar uma máscara binária da peça de vestuário. Esse modelo foi treinado com base em dados do **VITON HR** e **iMaterialist Fashion Dataset**. A escolha dessa arquitetura se deu pela capacidade de realizar uma segmentação precisa, crucial para isolar as roupas.

- **Dataset**: iMaterialist Fashion Dataset (disponível em: https://www.kaggle.com/c/imaterialist-fashion-2019-FGVC6)
- **Ferramenta de Segmentação**: Utilizamos a biblioteca **Cloths Segmentation** para realizar a segmentação. O modelo foi instalado via `pip install -U cloths_segmentation` e é capaz de processar imagens para gerar máscaras binárias.

#### Estimativa de Pose
Para a estimativa de pose, utilizamos o **PoseNet**, que detecta pontos-chave do corpo humano. O modelo foi implementado em Python e adaptado para maximizar a performance utilizando vetorização em NumPy/Scipy.

- **Modelo Utilizado**: PoseNet (implementação Python)
- **Biblioteca**: TensorFlow e OpenCV para processamento de imagem e captura de vídeos, caso necessário.

#### Composição de Imagens
O processo de composição final ocorre no script `main.py`, onde a máscara da roupa é combinada com a pose estimada, ajustando o tamanho e a posição da peça de roupa para que ela se encaixe na imagem da pessoa.

### 3. Apresentação da Base de Dados Utilizada
As bases de dados utilizadas para treinamento e teste incluem:
- **VITON HR Dataset**: Utilizado para treinar o modelo de segmentação de roupas.
- **iMaterialist Fashion Dataset**: Utilizado para testar a segmentação de diversas peças de vestuário.

## Requisitos Atendidos

### 1. Demonstração do Protótipo Funcional e Análise da Arquitetura de IA
- A segmentação de roupas, a estimativa de pose e a composição de imagens já estão implementadas e integradas ao protótipo. A arquitetura foi detalhadamente descrita acima, explicando a escolha dos modelos e suas implementações.

### 2. Organização e Estrutura da Documentação no GitHub
- Toda a documentação e o código do projeto estão organizados no GitHub, com descrições claras de cada etapa e instruções para execução do projeto.

### 3. Apresentação em Vídeo
- O vídeo de demonstração será gravado mostrando o fluxo completo do sistema, desde a entrada da imagem até o resultado final, explicando os detalhes técnicos e o funcionamento da IA.

## Entrega

### Arquivos Entregáveis
1. **Vídeo de Apresentação**: Link para o vídeo demonstrativo do protótipo funcional, detalhando as funcionalidades e a arquitetura da IA.
2. **Documentação do Projeto**: Um documento resumido em formato PDF (ou README.md), descrevendo o objetivo e a implementação do projeto.
3. **GitHub**: Link para o repositório do GitHub contendo a organização completa do projeto, código, e documentação.

### Condições de Entrega
- A entrega será realizada por meio dos links mencionados acima, assegurando que todos os arquivos estão íntegros e funcionando adequadamente.
  
---

## Links Importantes:
- **Dataset VITON HR**: [VITON HR Dataset no Google Drive](https://drive.google.com/drive/folders/0B8kXrnobEVh9fnJHX3lCZzEtd20yUVAtTk5HdWk2OVV0RGl6YXc0NWhMOTlvb1FKX3Z1OUk?resourcekey=0-OIXHrDwCX8ChjypUbJo4fQ&usp=sharing)
- **iMaterialist Fashion Dataset**: [Kaggle](https://www.kaggle.com/c/imaterialist-fashion-2019-FGVC6)
- **PoseNet Python Implementation**: [GitHub](https://github.com/rwightman/posenet-pytorch)
- **Detectron2**: [Facebook AI Research - Detectron2](https://github.com/facebookresearch/detectron2)

---

Esse README visa fornecer uma documentação completa e organizada do projeto, alinhando as funcionalidades do protótipo com os objetivos definidos.
