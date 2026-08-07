# 3ª Avaliação - Processamento Digital de Sinais

**Disciplina:** EECP0018 - Processamento Digital de Sinais  
**Curso:** Engenharia da Computação - UFMA  
**Professor:** Dr. Pedro Baptista Fernandes

**Integrantes:** Ana Iara Loayza Costa, José Victor Brito Costa e Milena Freire Britto Neves.

## Arquivos

| Arquivo | Conteúdo |
|---|---|
| `main.pdf` | Relatório completo em padrão ABNT |
| `main.tex` | Fonte LaTeX com cálculos e explicações digitadas |
| `referencias.bib` | Referências bibliográficas |
| `PDS_ATV3.ipynb` | Único arquivo de código, autossuficiente, com cálculos, simulações e gráficos |
| `images/` | Figuras geradas pelo código e usadas no relatório |

## Resultados principais

- Sinal: componentes de 10, 120 e 200 Hz; amostragem a 500 Hz sem aliasing.
- Analógico: Butterworth passa-baixas de ordem 3 e corte em 50 Hz.
- IIR: transformação bilinear com pré-distorção, corte digital exato em 50 Hz.
- FIR: ordem 40, 41 coeficientes, janela de Hamming e atraso de 20 amostras.
- Ambos atenuam fortemente as componentes acima de 50 Hz; o IIR requer menos operações e o FIR tem fase linear.

## Execução

Na pasta `avaliacao_3`, execute:

```bash
pip install numpy matplotlib jupyter
jupyter notebook PDS_ATV3.ipynb
```

O notebook usa somente NumPy e Matplotlib; as funções de projeto, resposta em frequência
e filtragem estão implementadas diretamente nele, sem depender de outro arquivo de código.

Para compilar o relatório:

```bash
pdflatex main.tex
bibtex main
pdflatex main.tex
pdflatex main.tex
```
