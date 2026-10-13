# FIAP — Fase 6: Visão Computacional

Projeto acadêmico desenvolvido para a **Fase 6 — O Começo da Rede Neural**, com foco em visão computacional e comparação entre diferentes abordagens de reconhecimento de imagens.

## Integrantes

- **Leandro Tenório** — RM 572083
- **João Pedro Iurovschi de Almeida Bessa** — RM 570160
- **Nícolas Xavier Costa** — RM 570336

**Curso:** Tecnologia em Inteligência Artificial  
**Instituição:** FIAP

## Objetivo

O projeto avalia três abordagens de visão computacional utilizando as classes **alicate** e **garrafa**:

1. **YOLO customizado** treinado com o dataset do projeto;
2. **YOLO tradicional** pré-treinado, sem adaptação às classes específicas;
3. **CNN treinada do zero** para classificação das imagens.

Também foram comparados dois treinamentos do YOLO customizado, com **30 e 60 épocas**.

## Dataset

O conjunto de dados contém **80 imagens**, sendo 40 imagens de cada classe.

| Conjunto | Alicate | Garrafa | Total |
|---|---:|---:|---:|
| Treinamento | 32 | 32 | 64 |
| Validação | 4 | 4 | 8 |
| Teste | 4 | 4 | 8 |

As imagens foram rotuladas no **Make Sense AI** e exportadas no formato YOLO.

## Resultados principais

### YOLO customizado

| Métrica | 30 épocas | 60 épocas |
|---|---:|---:|
| Precision | 1,000 | 0,978 |
| Recall | 0,963 | 0,967 |
| mAP@0.5 | 0,995 | 0,995 |
| mAP@0.5:0.95 | 0,822 | **0,920** |

O modelo de **60 épocas** apresentou o melhor resultado global, principalmente pela melhora do mAP@0.5:0.95.

### CNN do zero

- **Test Accuracy:** 1,0000
- **Test Loss:** 0,0043
- **Tempo médio de inferência:** aproximadamente 300,03 ms por imagem

Apesar do resultado de 100% no conjunto de teste, as curvas de treinamento indicaram **overfitting**, portanto o resultado deve ser interpretado com cautela devido ao tamanho reduzido do dataset.

### YOLO tradicional

O modelo pré-treinado foi aplicado diretamente às mesmas imagens de teste, sem customização. Ele não reconheceu corretamente as classes específicas do projeto, produzindo detecções como `keyboard`, `mouse`, `remote`, `cup`, `suitcase` e outras.

Esse resultado evidenciou a importância da adaptação do modelo ao domínio do problema.

## Comparação das abordagens

| Critério | YOLO customizado | YOLO tradicional | CNN do zero |
|---|---|---|---|
| Tipo de tarefa | Detecção | Detecção | Classificação |
| Classes específicas do projeto | Sim | Não | Sim |
| Resultado no teste | 8/8 corretas | 0/8 corretas nas classes desejadas | 8/8 corretas |
| Principal métrica | mAP50-95 = 0,920 | Não aplicável ao domínio | Accuracy = 1,000 |
| Tempo médio de inferência | ~147 ms/imagem | ~279,4 ms/imagem | ~300,03 ms/imagem |
| Necessidade de treinamento específico | Sim, com fine-tuning no dataset rotulado | Não | Sim, treinamento a partir do dataset do projeto |
| Tempo/esforço de customização | Médio: exige rotulação, configuração e treinamento | Baixo: uso imediato do modelo pré-treinado | Alto: exige organização por classes, definição da arquitetura, treinamento e avaliação |
| Facilidade de uso e integração | Alta após o treinamento; entrega diretamente classe, confiança e bounding box | Muito alta para uso genérico, porém limitada quando as classes do domínio não existem no treinamento original | Boa para classificação simples, mas exige lógica adicional quando é necessário localizar objetos |
| Localização do objeto | Sim | Sim | Não |
| Principal limitação | Dataset pequeno | Não conhece o domínio | Overfitting |

Os **tempos totais de treinamento** não foram utilizados como métrica numérica de comparação porque não foram registrados de forma padronizada entre os experimentos. Por isso, o custo de treinamento e customização foi comparado de forma **qualitativa**, considerando as etapas necessárias em cada abordagem.

A comparação mostra que a facilidade de uso isoladamente não é suficiente para definir a melhor solução. O YOLO tradicional possui integração imediata, mas seu conjunto de classes não representa adequadamente o problema. A CNN apresentou bom desempenho de classificação, porém não informa a posição do objeto na imagem. Para este projeto, o YOLO customizado apresentou o melhor equilíbrio entre adaptação ao domínio, localização e desempenho.

## Notebook

O notebook principal contém todo o processo de preparação do dataset, treinamento, validação, testes, métricas, gráficos e análise crítica.

**Arquivo:** [`LeandroTenorio_rm572083_pbl_fase6.ipynb`](https://github.com/TenorioDevfullStack/fiap-fase6-visao-computacional/blob/main/LeandroTenorio_rm572083_pbl_fase6.ipynb)

## Vídeo demonstrativo

O vídeo apresenta a estrutura do projeto, dataset utilizado, treinamento e resultados do YOLO customizado, CNN treinada do zero, comparação com o YOLO tradicional e as principais conclusões.

**Vídeo no YouTube (não listado):** [https://youtu.be/SOUztN6qEG0](https://youtu.be/SOUztN6qEG0)

## Limitações

- Dataset reduzido, com 80 imagens;
- apenas duas classes;
- poucos ambientes e condições de captura;
- conjuntos de validação e teste pequenos;
- sinais de overfitting na CNN;
- tempos de inferência dependentes do ambiente do Google Colab;
- tempos totais de treinamento não foram medidos sob um protocolo único e, portanto, não são comparados numericamente.

## Conclusão

Entre as abordagens avaliadas, o **YOLO customizado treinado por 60 épocas** apresentou o melhor equilíbrio entre desempenho, capacidade de localização dos objetos, adequação ao domínio e tempo de inferência.

Como continuidade, recomenda-se ampliar e diversificar o dataset e avaliar técnicas como **data augmentation, transfer learning, fine tuning e segmentação de imagens**.
