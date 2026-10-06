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
| Localização do objeto | Sim | Sim | Não |
| Principal limitação | Dataset pequeno | Não conhece o domínio | Overfitting |

## Notebook

O notebook principal contém todo o processo de preparação do dataset, treinamento, validação, testes, métricas, gráficos e análise crítica.

**Arquivo:** `LeandroTenorio_rm572083_pbl_fase6.ipynb`

> Após o upload do notebook para este repositório, o link direto deverá ser mantido nesta seção.

## Vídeo demonstrativo

O vídeo deve demonstrar, em até 5 minutos:

- estrutura do projeto;
- dataset utilizado;
- treinamento e resultados do YOLO customizado;
- CNN treinada do zero;
- comparação com o YOLO tradicional;
- principais conclusões.

**Link do vídeo no YouTube (não listado):** _adicionar após a gravação_.

## Limitações

- Dataset reduzido, com 80 imagens;
- apenas duas classes;
- poucos ambientes e condições de captura;
- conjuntos de validação e teste pequenos;
- sinais de overfitting na CNN;
- tempos de inferência dependentes do ambiente do Google Colab.

## Conclusão

Entre as abordagens avaliadas, o **YOLO customizado treinado por 60 épocas** apresentou o melhor equilíbrio entre desempenho, capacidade de localização dos objetos, adequação ao domínio e tempo de inferência.

Como continuidade, recomenda-se ampliar e diversificar o dataset e avaliar técnicas como **data augmentation, transfer learning, fine tuning e segmentação de imagens**.
