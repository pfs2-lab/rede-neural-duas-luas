# 🧠 Rede neural nas duas luas

Projeto final da disciplina **Matemática para Ciência de Dados** (Especialização em Ciência de Dados).

**Professor:** Adenilton · **Aluno:** Paulo Fraga · **Entrega:** 26/09/2026

📓 **Notebook:** [`projeto_rede_neural.ipynb`](projeto_rede_neural.ipynb). Ele já está executado, com todas as saídas e gráficos, e pode ser lido direto aqui no GitHub.

[![Abrir no Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/pfs2-lab/rede-neural-duas-luas/blob/main/projeto_rede_neural.ipynb)

## Objetivo

Projetar e implementar uma rede neural a partir do `exemplo4.py` visto em aula, escrevendo à mão, só com NumPy, as três peças do aprendizado: **forward**, **backpropagation** (regra da cadeia) e **gradiente descendente**.

## Modificações em relação ao `exemplo4.py`

| | `exemplo4.py` | Este trabalho |
|---|---|---|
| Implementação | nó por nó (escalar) | matricial (NumPy) |
| Neurônios ocultos | 2 | 2, 4, 8 e 16 |
| Ativação da camada oculta | sigmoid | **tanh** (comparada com sigmoid) |
| Base de dados | `make_moons`, 100 pontos, noise 0.1 | `make_moons`, 500 pontos, noise 0.2 |
| Avaliação | nos próprios dados de treino | treino/teste 70% / 30% |

## Estrutura do notebook

1. **Seção didática:** um neurônio separando dois grupos de pontos com uma reta (`make_blobs`)
2. **Um neurônio nas duas luas:** o limite de uma reta
3. **Rede com camada oculta:** forward matricial, backward, verificação do gradiente e treino
4. **Experimentos e conclusões:** número de neurônios e tanh × sigmoid

## Resultados

| Modelo | Parâmetros | Acurácia treino | Acurácia teste |
|---|---|---|---|
| 1 neurônio | 3 | 88% | 83% |
| 2-2-1, tanh (tamanho do `exemplo4.py`) | 9 | 90% | 87% |
| **2-4-1, tanh** | **17** | **98%** | **94,5%** |
| 2-8-1, tanh | 33 | 98% | 95% |
| 2-16-1, tanh | 65 | 99% | 96% |
| 2-8-1, sigmoid | 33 | 98% | 94,5% |

*Redes com camada oculta: média de 5 inicializações (seeds 0 a 4), taxa 0,01 e 5000 épocas.*

**Principais conclusões:**

- Um único neurônio só desenha uma reta e para em ~88% nas luas, por falta de capacidade e não de treino.
- Com uma camada oculta, cada neurônio desenha uma reta e a saída combina essas retas numa fronteira curva: com 4 neurônios, o teste sobe de 83% para ~95%.
- Mais neurônios ajudam até certo ponto; o erro que sobra vem do ruído na região em que as luas se sobrepõem.
- A tanh aprende mais rápido que a sigmoid na camada oculta, porque a derivada dela é maior (até 1, contra 0,25).
- O backward foi conferido com a derivada numérica (verificação do gradiente).

## Como rodar

No Colab: clique no botão **Abrir no Colab** acima e use *Ambiente de execução → Executar tudo*.

Localmente:

```bash
pip install -r requirements.txt
jupyter notebook projeto_rede_neural.ipynb
```
