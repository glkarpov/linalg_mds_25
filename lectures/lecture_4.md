---
title: "Линейная алгебра"
subtitle: "Линейная зависимость и независимость. Базис."
institute: "Прикладные нейросетевые технологии, ФКН ВШЭ"
author: "Глеб Карпов"
format: 
    beamer:
        pdf-engine: xelatex
        aspectratio: 169
        fontsize: 9pt
        theme: Singapore
        fonmttheme: serif
        section-titles: true
        incremental: false
        include-in-header: ../files/xeheader.tex  # Custom LaTeX commands and preamble
---

## Зависимость и независимость векторов
### Мотивация

- Рассмотрим набор векторов $\{v_1, \ldots, v_m\}$, заранее извлеченных из $\mathbb{V}$, и произвольный набор скаляров $\alpha_1, \ldots, \alpha_m$ из $\mathbb{R}$. В результате построения линейной комбинации получим некий элемент $x \in \mathbb{V}$:
$$
    x = \alpha_1 v_1 + \ldots + \alpha_m v_m
$$

- Уникален ли такой набор $\{\alpha_1, \ldots, \alpha_m\}$ или, может, существует другой
набор $\{\tilde{\alpha}_1, \ldots, \tilde{\alpha}_m\}$ такой, что:
$$
    x = \tilde{\alpha}_1 v_1 + \ldots + \tilde{\alpha}_m v_m.
$$

- **Пример из жизни (БЖУ — белки, жиры, углеводы):**
$\textcolor{red}{p}=(100, 50, 100)^T$ — плов,
$\textcolor{blue}{r}=(0, 50, 100)^T$ — рис,
$\textcolor{green!60!black}{g}=(100, 0, 0)^T$ — грудка.

- Цель $\begin{pmatrix} 200 \\ 50 \\ 100 \end{pmatrix}$ достигается по-разному:
$$
    1 \cdot \textcolor{red}{p} + 1 \cdot \textcolor{green!60!black}{g} = 1 \cdot \textcolor{blue}{r} + 2 \cdot \textcolor{green!60!black}{g} = \begin{pmatrix} 200 \\ 50 \\ 100 \end{pmatrix}
$$

## Зависимость и независимость векторов
### Мотивация

- Давайте предположим, что набор не уникален, и вычтем два равенства друг из друга:
\begin{multline*}
    (x - x) = \mathbf{0} = (\alpha_1 - \tilde{\alpha}_1) v_1 + (\alpha_2 - \tilde{\alpha}_2) v_2 + \ldots + (\alpha_m - \tilde{\alpha}_m) v_m \\
    = \gamma_1 v_1 + \gamma_2 v_2  + \ldots + \gamma_m v_m
\end{multline*}

- Задача уникальности представления $x$ теперь изменилась к задаче "как получить элемент 0" в результате линейной комбинации.

- Если единственный возможный вариант получить $\mathbf{0}$ это положить все $\gamma_i = 0$:
$$
   \forall i: \, (\alpha_i - \tilde{\alpha}_i) = 0 \rightarrow \alpha_i = \tilde{\alpha}_i.
$$
Что будет означать, что представление $x$ уникально.

- Если есть какой-то другой способ получить $\mathbf{0}$, т.е. хотя бы один $\gamma_k \neq 0$, значит
$(\alpha_k - \tilde{\alpha}_k) \neq 0 \rightarrow \alpha_k \neq \tilde{\alpha}_k$. Что означает, что представление $x$ не уникально - существует другой набор коэффициентов.

## Линейная независимость
### Определение
Мы назовем набор векторов \textit{линейно независимым}, если единственная возможность получить элемент $\mathbf{0}$ как результат линейной комбинации:

$$
    \gamma_1 v_1 + \ldots + \gamma_m v_m = \mathbf{0},
$$

это положить все скаляры равными $0$, $\gamma_1 = \ldots = \gamma_m = 0$. (Также называется \textit{тривиальной комбинацией}).

## Линейная независимость
### Примеры

::: {.columns}

::: {.column width="50%"}

БЖУ (белки, жиры, углеводы), г:

$\textcolor{red}{g}=(100, 0, 0)^T$ — грудка,

$\textcolor{blue}{m}=(0, 100, 0)^T$ — масло,

$\textcolor{green!60!black}{r}=(0, 50, 100)^T$ — рис

Единственный способ получить $\mathbf{0}$:
\begin{gather*}
    \gamma_1 \cdot \textcolor{red}{\begin{pmatrix} 100 \\ 0 \\ 0 \end{pmatrix}} + \gamma_2 \cdot \textcolor{blue}{\begin{pmatrix} 0 \\ 100 \\ 0 \end{pmatrix}} + \gamma_3 \cdot \textcolor{green!60!black}{\begin{pmatrix} 0 \\ 50 \\ 100 \end{pmatrix}} = \mathbf{0} \\
    \Rightarrow \gamma_1 = \gamma_2 = \gamma_3 = 0
\end{gather*}
Набор линейно независим.

:::

::: {.column width="50%"}

Пример: $\mathbb{R}[x, 2]$

$\textcolor{red}{p_1}(x) = x^2$, $\textcolor{blue}{p_2}(x) = x$, $\textcolor{green}{p_3}(x) = 1$

Тривиальная комбинация даёт нулевой полином:
$$
    \gamma_1 x^2 + \gamma_2 x + \gamma_3 \cdot 1 = 0 \Rightarrow \gamma_1 = \gamma_2 = \gamma_3 = 0
$$
Набор $\{x^2, x, 1\}$ линейно независим.

:::

:::

## Линейная зависимость
### Определение
С другой стороны, мы назовем набор векторов \textit{линейно зависимым}, если **существует** нетривиальная комбинация коэффициентов $\gamma_1, \ldots, \gamma_m$, (не равные $0$ одновременно), такая что:

$$
    \gamma_1 v_1 + \ldots + \gamma_m v_m = \mathbf{0}.
$$

## Линейная зависимость
### Примеры

::: {.columns}

::: {.column width="50%"}

Пример: $\mathbb{R}^2$

$\textcolor{red}{a}=\begin{pmatrix}1\\1\end{pmatrix}$,
$\textcolor{blue}{b}=\begin{pmatrix}2\\2\end{pmatrix}$,
$\textcolor{green!60!black}{c}=\begin{pmatrix}0\\1\end{pmatrix}$

Нетривиальная комбинация:
\begin{gather*}
    2 \cdot \textcolor{red}{a} + (-1) \cdot \textcolor{blue}{b} + 0 \cdot \textcolor{green!60!black}{c} = \mathbf{0}
\end{gather*}
(вектор $b$ — удвоенный $a$). Набор линейно зависим.

:::

::: {.column width="50%"}

Пример: $\mathbb{R}[x, 2]$

$\textcolor{red}{p_1}(x) = x^2$, $\textcolor{blue}{p_2}(x) = x^2 + x$, $\textcolor{green}{p_3}(x) = x$

$$
    (-1) \cdot \textcolor{red}{p_1} + 1 \cdot \textcolor{blue}{p_2} + (-1) \cdot \textcolor{green}{p_3} = -(x^2) + (x^2 + x) - x = 0
$$
Набор линейно зависим.

:::

:::

## Базис
### Определение

- Набор векторов $v_1, \ldots, v_n$ из $\mathbb{V}$ называется _базисом_ пространства $\mathbb{V}$ тогда и только тогда, когда _любой_ вектор $x \in \mathbb{V}$ может быть уникально представлен в форме линейной комбинации:
$$
    x = \alpha_1 v_1 + \ldots + \alpha_n v_n.
$$

- Соответствующие уникальные коэффициенты $\alpha_1, \ldots, \alpha_n$ мы называем _координатами_ вектора $x$ в базисе $(v_1, \ldots, v_n)$.

- Немного иначе: набор векторов $v_1, \ldots, v_n$ из $\mathbb{V}$ называется _базисом_ пространства $\mathbb{V}$ тогда и только тогда, когда этот набор векторов линейно независим и $\text{span} (v_1, \ldots, v_n) = \mathbb{V}$, то есть мы можем 'дотянуться' до любого элемента из $\mathbb{V}$.

## Базис. Примеры

### Пример в координатном векторном пространстве

- Координатное пространство $\mathbb{R}^2$. Возьмем вектор, например, $x = \vtwo{5}{2}$:

\begin{align*}
\vtwo{5}{2} & = \textcolor{violet}{5} \vtwo{1}{0} + \textcolor{violet}{2} \vtwo{0}{1}, \quad [x]_S = \vtwo{\textcolor{violet}{5}}{\textcolor{violet}{2}}, \quad S = \left\{\vtwo{1}{0}, \, \vtwo{0}{1} \right\} \\
\vtwo{5}{2} & = \textcolor{violet}{0.5} \vtwo{2}{4} + \textcolor{violet}{-0.5} \vtwo{-8}{0}, \quad [x]_B = \vtwo{\textcolor{violet}{0.5}}{\textcolor{violet}{-0.5}}, \quad B = \left\{\vtwo{2}{4}, \, \vtwo{-8}{0} \right\} \\
\vtwo{5}{2} & = \textcolor{violet}{-0.25} \vtwo{-8}{2} + \textcolor{violet}{-5.5} \vtwo{0}{-1}, \quad [x]_C = \vtwo{\textcolor{violet}{-0.25}}{\textcolor{violet}{-5.5}}, \quad C = \left\{\vtwo{-8}{2}, \, \vtwo{0}{-1} \right\} \\
\end{align*}

## Базис. Примеры
### Пример в пространстве матриц

- Пространство $\mathbb{R}^{2 \times 2}$. Возьмём матрицу $X = \begin{pmatrix} 3 & 1 \\ 2 & 0 \end{pmatrix}$:

\begin{align*}
X &= \textcolor{violet}{3}\begin{pmatrix}1&0\\0&0\end{pmatrix}
 + \textcolor{violet}{1}\begin{pmatrix}0&1\\0&0\end{pmatrix}
 + \textcolor{violet}{2}\begin{pmatrix}0&0\\1&0\end{pmatrix}
 + \textcolor{violet}{0}\begin{pmatrix}0&0\\0&1\end{pmatrix}, \\
&\quad [X]_S = \begin{pmatrix}\textcolor{violet}{3}\\\textcolor{violet}{1}\\\textcolor{violet}{2}\\\textcolor{violet}{0}\end{pmatrix},
\quad S = \left\{
\begin{pmatrix}1&0\\0&0\end{pmatrix},\,
\begin{pmatrix}0&1\\0&0\end{pmatrix},\,
\begin{pmatrix}0&0\\1&0\end{pmatrix},\,
\begin{pmatrix}0&0\\0&1\end{pmatrix}
\right\}
\end{align*}

\begin{align*}
X &= \textcolor{violet}{1.5}\begin{pmatrix}1&0\\0&1\end{pmatrix}
 + \textcolor{violet}{1}\begin{pmatrix}0&1\\0&0\end{pmatrix}
 + \textcolor{violet}{2}\begin{pmatrix}0&0\\1&0\end{pmatrix}
 + \textcolor{violet}{1.5}\begin{pmatrix}1&0\\0&-1\end{pmatrix}, \\
&\quad [X]_B = \begin{pmatrix}\textcolor{violet}{1.5}\\\textcolor{violet}{1}\\\textcolor{violet}{2}\\\textcolor{violet}{1.5}\end{pmatrix},
\quad B = \left\{
\begin{pmatrix}1&0\\0&1\end{pmatrix},\,
\begin{pmatrix}0&1\\0&0\end{pmatrix},\,
\begin{pmatrix}0&0\\1&0\end{pmatrix},\,
\begin{pmatrix}1&0\\0&-1\end{pmatrix}
\right\}
\end{align*}

## Базис. Примеры
### Пример в векторном пространстве полиномов

- Векторное пространство $\mathbb{R}[x,2]$. Возьмём $f(x) = 2x^2 - 7x + 4$:

\begin{align*}
f(x) & = \textcolor{violet}{2} \cdot x^2 + \textcolor{violet}{-7} \cdot x + \textcolor{violet}{4} \cdot 1, \quad [f]_S = \vthree{\textcolor{violet}{2}}{\textcolor{violet}{-7}}{\textcolor{violet}{4}}, \quad S = \left\{x^2, \, x , \, 1 \right\} \\
f(x) & = \textcolor{violet}{0.5} \cdot (4x^2 - 2x) + \textcolor{violet}{-2} \cdot (3x) + \textcolor{violet}{0.5} \cdot 8, \quad [f]_B = \vthree{\textcolor{violet}{0.5}}{\textcolor{violet}{-2}}{\textcolor{violet}{0.5}}, \quad B = \left\{4x^2 - 2x, \, 3x , \, 8 \right\}
\end{align*}

## Базис. Примеры
### Ещё один базис в пространстве полиномов

- Тот же $f(x) = 2x^2 - 7x + 4$, другие базисы:

\begin{align*}
f(x) & = \textcolor{violet}{1} \cdot (2x^2) + \textcolor{violet}{-7} \cdot (x+1) + \textcolor{violet}{11} \cdot 1, \quad [f]_C = \vthree{\textcolor{violet}{1}}{\textcolor{violet}{-7}}{\textcolor{violet}{11}}, \quad C = \left\{2x^2, \, x+1 , \, 1 \right\} \\
f(x) & = \textcolor{violet}{2} \cdot (x^2 + x) + \textcolor{violet}{-9} \cdot (x+1) + \textcolor{violet}{13} \cdot 1, \quad [f]_D = \vthree{\textcolor{violet}{2}}{\textcolor{violet}{-9}}{\textcolor{violet}{13}}, \quad D = \left\{x^2 + x, \, x+1 , \, 1 \right\}
\end{align*}

## Базис. Примеры
### Контрпример: зависимый набор

- Зависимый набор из $\mathbb{R}^2$:
$\textcolor{red}{a}=\vtwo{1}{1}$, $\textcolor{blue}{b}=\vtwo{2}{2}$
не является базисом $\mathbb{R}^2$: $\operatorname{span}\{a,b\}$ — лишь прямая, а не вся плоскость
(и представление любого вектора с этой прямой не единственно).

## Важный промежуточный вывод

::: {.columns}

::: {.column width="50%"}

\begin{tikzpicture}[scale=1.0]
% Центральный вектор
\node[draw, rectangle, minimum width=1.5cm, minimum height=2cm, fill=blue!20] (vector) at (0,0) {
\begin{minipage}{1.2cm}
\centering
$\begin{pmatrix}
x_1 \\
x_2 \\
\vdots \\
x_n
\end{pmatrix}$
\end{minipage}
};

% Векторные пространства - круги
\node[draw, circle, minimum size=2cm, fill=red!20] (polynomials) at (-3, 2) {
\begin{minipage}{1.8cm}
\centering
\textbf{Полиномы}\\
$p(x) = a_0 + a_1x + \ldots + a_{n-1}x^{n-1}$
\end{minipage}
};

\node[draw, circle, minimum size=2cm, fill=green!20] (matrices) at (3, 2) {
\begin{minipage}{1.8cm}
\centering
\textbf{Матрицы}\\
$A = \begin{pmatrix}
a_{11} & a_{12} \\
a_{21} & a_{22}
\end{pmatrix}$
\end{minipage}
};

\node[draw, circle, minimum size=2cm, fill=yellow!20] (functions) at (0, 3.5) {
\begin{minipage}{1.8cm}
\centering
\textbf{Функции}\\
$f: \mathbb{R} \to \mathbb{R}$
\end{minipage}
};

% Стрелки от пространств к вектору
\draw[thick, ->] (polynomials) -- (vector);
\draw[thick, ->] (matrices) -- (vector);
\draw[thick, ->] (functions) -- (vector);

% Подпись
\node[below] at (0, -1.) {\textbf{Линейная алгебра: единый язык для разных объектов}};

\end{tikzpicture}

:::

::: {.column width="50%"}

\begin{itemize}
    \item Если векторное пространство $\mathbb{V}$ имеет базис $\mathbf{v}_1, \ldots, \mathbf{v}_n$, то любой вектор $\mathbf{v}$ однозначно определяется своими координатами $\alpha_k$ в этом базисе. Если мы упакуем $\alpha_k$ в вектор из $\mathbb{R}^n$, то можем оперировать им вместо оперирования над $\mathbf{v}$.

    \item Если $\mathbf{v}=\sum_{k=1}^n \alpha_k \mathbf{v}_k$ и $\mathbf{w}=\sum_{k=1}^n \beta_k \mathbf{v}_k$, то
$$
\mathbf{v}+\mathbf{w}=\sum_{k=1}^n \alpha_k \mathbf{v}_k+\sum_{k=1}^n \beta_k \mathbf{v}_k=\sum_{k=1}^n\left(\alpha_k+\beta_k\right) \mathbf{v}_k
$$
т.е. вместо сложения двух оригинальных векторов, можно сложить векторы координат. 

\item Аналогично, чтобы получить $\alpha \mathbf{v}$, можно умножить столбец координат $\mathbf{v}$ на $\alpha$ и сразу получить координаты вектора $\alpha \mathbf{v}$.
\end{itemize}

:::

:::
