# 1ª Avaliação — Processamento Digital de Sinais

**Disciplina:** EECP0018 - Processamento Digital de Sinais
**Curso:** Engenharia da Computação — UFMA
**Professor:** Dr. Pedro Baptista Fernandes

**Integrantes do grupo:**

- Ana Iara Loayza Costa — [@iaraloayza](https://github.com/iaraloayza)
- José Victor Brito Costa — [@josevbrito](https://github.com/josevbrito)
- Milena Freire Britto Neves — [@milenafbn](https://github.com/milenafbn)

---

## Conteúdo desta pasta

| Arquivo | Descrição |
|---------|-----------|
| `PDS_ATV1.ipynb` | Notebook com a resolução e o código de **todas as questões (1 a 5)** |
| `main.tex` | Relatório em LaTeX com as deduções matemáticas e os gráficos |
| `images/` | Gráficos gerados pelo notebook e usados no relatório |

---

## Como rodar o notebook

O notebook foi desenvolvido para o **Google Colab** (usa `google.colab.files`
para baixar os gráficos), mas roda em qualquer ambiente com Python 3.

### Opção 1 — Google Colab (recomendada)

1. Acesse [colab.research.google.com](https://colab.research.google.com).
2. Menu **Arquivo → Fazer upload de notebook** e selecione `PDS_ATV1.ipynb`.
3. Menu **Ambiente de execução → Executar tudo** (ou `Ctrl+F9`).
4. Os gráficos são gerados e salvos automaticamente na pasta `images/`
   (criada pela primeira célula do notebook).

### Opção 2 — Localmente (Jupyter)

```bash
pip install numpy matplotlib jupyter
jupyter notebook PDS_ATV1.ipynb
```

Rode as células em ordem. A primeira célula cria a pasta `images/` e todos os
gráficos são salvos lá automaticamente (`plt.savefig`), já prontos para o
relatório LaTeX — não é preciso mover nada manualmente.

### Dependências

Apenas `numpy` e `matplotlib`. Nenhuma função pronta de convolução ou de
resposta em frequência foi utilizada — tudo foi implementado manualmente,
conforme pedido no enunciado.

---

## Relatório em PDF

O relatório já compilado está em **`main.pdf`** — basta abri-lo.

Para recompilar a partir do fonte, com uma distribuição LaTeX instalada
(TeX Live, MiKTeX, Overleaf...):

```bash
pdflatex main.tex
```

Os gráficos referenciados estão na pasta `images/`, então mantenha essa pasta
ao lado do `main.tex`. No **Overleaf**, basta enviar o `main.tex` junto com a
pasta `images/`.

---

## Roteiro das questões

| Questão | Tema | O que foi feito |
|---------|------|-----------------|
| **1** | Periodicidade de sinais discretos | Verificação do período $N=5$ de $\cos(12\pi n/5)$ e efeito de multiplicar a frequência por 2 e por 5 |
| **2** | `Deslocamento_Tempo(x, n, n0)` | Função que retorna $y[n] = x[n-n_0]$ para qualquer $x$, $n$ e $n_0$ |
| **3** | `Convolucao(x, h)` | Convolução de sistemas causais implementada do zero (sem `np.convolve`) |
| **4** | `Investimento(y0, r, x, n)` | Solução fechada (não recursiva) da equação de diferenças do saldo |
| **5** | $H(z)$ e resposta em frequência | Função de transferência, gráficos de magnitude/fase e saída para $x[n]=\cos(\pi n/4)$ |

---

## Resumo para a apresentação

1. **Questão 1** — Mostrar que, no tempo discreto, dobrar a frequência **não**
   necessariamente muda o período ($N=5$ nos dois casos), e que multiplicar por
   5 torna o sinal constante ($N=1$). Diferença fundamental em relação ao caso
   contínuo.
2. **Questão 2** — Explicar que a função busca $x$ no índice $n-n_0$ e preenche
   com zero fora do domínio, mantendo $x$ e $y$ no mesmo eixo $n$.
3. **Questão 3** — Destacar a soma dupla $y[k+m] \mathrel{+}= x[k]\,h[m]$ como
   implementação direta da definição de convolução; conferir com o exemplo
   $\{1, 2{,}5, 4, 1{,}5\}$.
4. **Questão 4** — Enfatizar que a solução é **fechada** (fórmula fechada, não
   iteração), com o exemplo dando R\$ 3.663,33.
5. **Questão 5** — Deduzir $H(z)$ passo a passo; confirmar a estabilidade pela
   RDC ($|z| > 0{,}837$ contém o círculo unitário, por isso $H(e^{j\omega})$
   existe); caracterizar o sistema como **filtro passa-baixas** (ganho $1{,}03$
   em $\omega=0$, $0{,}0012$ em $\omega=\pi$); e mostrar que em $\omega=\pi/4$
   o ganho é $0{,}139$ com fase $-3{,}051$ rad — quase inversão. Vale destacar
   que a saída analítica foi **validada** contra a iteração direta da equação
   de diferenças (erro $\sim 10^{-16}$).
