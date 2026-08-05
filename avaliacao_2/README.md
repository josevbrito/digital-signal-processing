# 2ª Avaliação - Processamento Digital de Sinais

**Disciplina:** EECP0018 - Processamento Digital de Sinais
**Curso:** Engenharia da Computação - UFMA
**Professor:** Dr. Pedro Baptista Fernandes

**Integrantes do grupo:**

- Ana Iara Loayza Costa — [@iaraloayza](https://github.com/iaraloayza)
- José Victor Brito Costa — [@josevbrito](https://github.com/josevbrito)
- Milena Freire Britto Neves — [@milenafbn](https://github.com/milenafbn)

---

## Conteúdo desta pasta

| Arquivo             | Descrição                                                                      |
| ------------------- | -------------------------------------------------------------------------------- |
| `main.pdf`        | **Relatório completo** (formatação ABNT) — responde às duas questões |
| `main.tex`        | Fonte LaTeX do relatório (classe`abntex2`)                                    |
| `referencias.bib` | Bibliografia em BibTeX (NBR 6023)                                                |
| `PDS_ATV2.ipynb`  | Notebook com o código da Questão 2                                             |
| `images/`         | Gráficos gerados pelo notebook + brasão da UFMA                                |

---

## As duas questões

### Questão 1 (7,0 pontos) — Pesquisa

Desenvolvida nos capítulos 2 a 6 do `main.pdf`, cobrindo os quatro tópicos pedidos:

| Tópico do enunciado                                              | Onde está |
| ----------------------------------------------------------------- | ---------- |
| i) Definição da SFTD e da TFTD + características dos espectros | Cap. 2 e 3 |
| ii) Propriedades da TFTD                                          | Cap. 4     |
| iii) Ligação entre a TFTD e a transformada$z$                 | Cap. 5     |
| iv) O que é a Transformada Rápida de Fourier                    | Cap. 6     |

### Questão 2 (3,0 pontos) — Código

Desenvolvida no Cap. 7 do relatório e implementada em `PDS_ATV2.ipynb`.

O sinal do enunciado é o pulso retangular $x[n] = 1$ para $-4 \le n \le 4$. Sua TFTD é
o **núcleo de Dirichlet**:

$$
X_M(e^{j\omega}) = \frac{\mathrm{sen}(\omega L/2)}{\mathrm{sen}(\omega/2)}, \qquad L = 2M+1
$$

O código está **generalizado**: basta alterar a variável `M` para mudar a largura do
sinal (o caso do enunciado é `M = 4`).

---

## Como rodar o notebook

### Opção 1 — Google Colab

1. Acesse [colab.research.google.com](https://colab.research.google.com).
2. **Arquivo → Fazer upload de notebook** e selecione `PDS_ATV2.ipynb`.
3. **Ambiente de execução → Executar tudo** (`Ctrl+F9`).

### Opção 2 — Localmente

```bash
pip install numpy matplotlib jupyter
jupyter notebook PDS_ATV2.ipynb
```

Os gráficos são salvos automaticamente em `images/`, já prontos para o relatório.

**Dependências:** apenas `numpy` e `matplotlib`.

---

## Como compilar o relatório

O relatório já vem compilado em `main.pdf`. Para recompilar é preciso uma distribuição
LaTeX com a classe **`abntex2`** instalada:

```bash
pdflatex main.tex
bibtex   main
pdflatex main.tex
pdflatex main.tex
```

As três passadas são necessárias para resolver as citações, o sumário e as referências
cruzadas. No **Overleaf**, basta enviar `main.tex`, `referencias.bib` e a pasta
`images/`, e selecionar o compilador pdfLaTeX (a classe `abntex2` já está disponível lá).

---

## Sobre a validação numérica

O espectro é calculado por **três caminhos independentes**, o que permite verificação
cruzada:

1. **Pela definição** — somatório direto $\sum_n x[n]e^{-j\omega n}$, sem funções prontas;
2. **Pela forma fechada** — núcleo de Dirichlet deduzido analiticamente;
3. **Pela FFT** — `numpy.fft.fft` com *zero-padding*, conforme facultado pelo enunciado.

Os três concordam com erro da ordem de $10^{-14}$, e o **teorema de Parseval** é
verificado com erro de $1{,}8 \times 10^{-15}$.

---

## Resumo para a apresentação

1. **SFTD × TFTD** — a ideia central é a dualidade: *periodicidade em um domínio vira
   discretização no outro*. Sinal periódico → espectro discreto (só $N$ raias); sinal
   aperiódico → espectro contínuo. Em ambos, o espectro é periódico — marca registrada
   do tempo discreto.
2. **Propriedades** — destacar a da **convolução** (convolução no tempo vira produto em
   frequência: é a base da filtragem digital) e sua dual, a da **multiplicação**, que
   explica o espalhamento espectral ao truncar um sinal.
3. **Ligação com a transformada $z$** — $X(e^{j\omega}) = X(z)|_{z=e^{j\omega}}$: a TFTD
   é a transformada $z$ sobre a circunferência unitária. Daí sai de graça o critério de
   existência (a RDC precisa conter $|z|=1$) e a conexão com estabilidade.
4. **FFT** — não é outra transformada: é um **algoritmo** para a DFT. Sai de $O(N^2)$
   para $O(N\log_2 N)$ — 683× mais rápido já em $N = 4096$.
5. **Código** — mostrar o gráfico do efeito da largura: pulso mais largo no tempo →
   lóbulo mais estreito em frequência. É a relação inversa entre os domínios.
