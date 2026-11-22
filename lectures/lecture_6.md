---
title: "Линейная алгебра"
subtitle: "СЛУ для анализа векторов"
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

## СЛУ для анализа векторов
### Линейная оболочка и единственность решения
- Наш взгляд на mat-vec как на линейную комбинацию столбцов матрицы приводит нас к более глубокому понимания СЛУ. Если обозначим столбцы матрицы за $a_1, \ldots, a_m$ то тогда:
\begin{equation*}
    A \mathbf{x} = r \leftrightarrow x_1 a_1 + \ldots + x_m a_m = r,
\end{equation*}
Решить СЛУ теперь означает подобрать коэффициенты для линейной комбинации столбцов матрицы, чтобы получился right-hand side вектор $r$. Но важным фактором является то, чтобы с помощью векторов $a_1, \ldots, a_m$ вообще можно было бы "дотянуться" до вектора $r$. Иными словами, получаем:
- ::: {.callout-note}
### Существование решения
Для того, чтобы у СЛУ $A \mathbf{x} = r$ существовало хотя бы одно решение, необходимо, чтобы выполнялось:
\begin{equation*}
    r \in \text{ span } (a_1, \ldots, a_m)
\end{equation*}
Иначе, СЛУ называется несовместной (inconsistent).
В ступенчатом виде матрицы несовместность системы выражается в виде наличия строчки:
$$
    \left[ 0 \; 0 \; \ldots \; 0  \;| \; b \right], \; b \neq 0
$$
:::

## Пример: несовместность vs неуникальное решение

- $\left(\begin{array}{c c c|c} 1 & 0 & 1 & 1 \\ 0 & 1 & 1 & 1 \\ 1 & 1 & 2 & 3 \end{array}\right)$

- $\left(\begin{array}{c c c|c} 1 & 0 & 1 & 1 \\ 0 & 1 & 1 & 2 \\ 1 & 1 & 2 & 3 \end{array}\right)$

## Пример: несовместная система

$$
\left(\begin{array}{c c c|c}
1 & 0 & 1 & 1 \\
0 & 1 & 1 & 1 \\
1 & 1 & 2 & 3
\end{array}\right)
\xrightarrow{R_3 - R_1 - R_2}
\left(\begin{array}{c c c|c}
1 & 0 & 1 & 1 \\
0 & 1 & 1 & 1 \\
0 & 0 & 0 & 1
\end{array}\right)
$$

Строка $(0\ 0\ 0 \mid 1)$ — это $0 = 1$. Решений нет.

Вектор правой части лежит вне линейной оболочки векторов-столбцов матрицы.
До него невозможно добраться, какие бы коэффициенты мы ни
перебирали.

## Пример: бесконечно много решений

Та же матрица, но теперь в правой части одна замена: $1 \to 2$ во второй строке.

$$
\left(\begin{array}{c c c|c}
1 & 0 & 1 & 1 \\
0 & 1 & 1 & 2 \\
1 & 1 & 2 & 3
\end{array}\right)
\xrightarrow{R_3 - R_1 - R_2}
\left(\begin{array}{c c c|c}
1 & 0 & 1 & 1 \\
0 & 1 & 1 & 2 \\
0 & 0 & 0 & 0
\end{array}\right)
$$

Теперь вектор правой части лежит в линейной оболочке столбцов матрицы, теперь до него можно добраться. Но так как есть свободная переменная, можно добраться бесконечным количеством способов.

$$
x_1 = 1 - t,\quad x_2 = 2 - t,\quad x_3 = t,
\qquad
X = \begin{pmatrix}1 \\ 2 \\ 0\end{pmatrix} + t\begin{pmatrix}-1 \\ -1 \\ 1\end{pmatrix},\quad t \in \mathbb{R}.
$$

## Reminder: в чем сила?

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

## СЛУ как способ исследовать наборы векторов
- Для отдельного рассмотрения можно вынести системы однородных линейных уравнений вида $A \mathbf{x} = \mathbf{0}$

- В интерпретации линейной комбинации столбцов такие уравнения внезапно напоминают нам про возможность получения нулевого вектора:
\begin{equation*}
    A \mathbf{x} = \mathbf{0} \leftrightarrow x_1 a_1 + \ldots + x_m a_m = \mathbf{0},
\end{equation*}
Если единственное решение - тривиальный вектор $\mathbf{x} = \mathbf{0}$, то набор перед нами линейно независимая группа векторов в столбцах матрицы. Иначе - линейно зависимая.

## Пример

Найдите \textit{все} решения векторного уравнения
\begin{equation*}
x_1 \mathbf{v}_1 + x_2 \mathbf{v}_2 + x_3 \mathbf{v}_3 = \mathbf{0},
\end{equation*}
где
$\mathbf{v}_1 = (1,\, 1,\, 0)^T$,
$\mathbf{v}_2 = (0,\, 1,\, 1)^T$,
$\mathbf{v}_3 = (1,\, 0,\, 1)^T$.
Какой вывод можно сделать о линейной независимости
(зависимости) системы векторов $\mathbf{v}_1, \mathbf{v}_2, \mathbf{v}_3$?

## СЛУ как способ исследовать наборы векторов
::: {.callout-note}
### Утверждение
Пусть у нас есть набор векторов $\mathbf{v}_1, \mathbf{v}_2, \ldots, \mathbf{v}_m \in \mathbb{R}^n$, и пусть $A=\left[\mathbf{v}_1, \mathbf{v}_2, \ldots, \mathbf{v}_m\right]$ — это матрица размера $n \times m$ со столбцами $\mathbf{v}_1, \mathbf{v}_2, \ldots, \mathbf{v}_m$. Тогда
\begin{enumerate}
    \item Система $\mathbf{v}_1, \mathbf{v}_2, \ldots, \mathbf{v}_m$ линейно независима тогда и только тогда, когда ступенчатая форма матрицы $A$ имеет ведущий элемент в каждом столбце;
    \item Линейная оболочка системы $\mathbf{v}_1, \mathbf{v}_2, \ldots, \mathbf{v}_m$ совпадает с $\mathbb{R}^n$ тогда и только тогда, когда ступенчатая форма матрицы $A$ имеет ведущий элемент в каждой строке;
    \item Система $\mathbf{v}_1, \mathbf{v}_2, \ldots, \mathbf{v}_m$ является базисом в $\mathbb{R}^n$ тогда и только тогда, когда ступенчатая форма матрицы $A$ имеет ведущий элемент в каждом столбце и в каждой строке.
\end{enumerate}
:::

## Пример

При каком значении $b$ система
\begin{equation*}
\begin{pmatrix}
1 & 2 & 2 \\
2 & 4 & 6 \\
1 & 2 & 3
\end{pmatrix}
\mathbf{x}
=
\begin{pmatrix}
1 \\ 4 \\ b
\end{pmatrix}
\end{equation*}
имеет решение? Найдите общее решение системы при этом значении $b$.

## Пример

Определите, линейно независимы ли векторы
\begin{equation*}
\begin{pmatrix}1 \\ 1 \\ 0 \\ 0\end{pmatrix},\;
\begin{pmatrix}1 \\ 0 \\ 1 \\ 0\end{pmatrix},\;
\begin{pmatrix}0 \\ 0 \\ 1 \\ 1\end{pmatrix},\;
\begin{pmatrix}0 \\ 1 \\ 0 \\ 1\end{pmatrix}.
\end{equation*}
Совпадает ли их линейная оболочка с $\mathbb{R}^4$?

## Пример

Какие из следующих систем векторов являются базисами в $\mathbb{R}^3$?
\begin{enumerate}
    \item[(a)]
    $(1,\, 2,\, -1)^T$,\quad
    $(1,\, 0,\, 2)^T$,\quad
    $(2,\, 1,\, 1)^T$;
    \item[(b)]
    $(-1,\, 3,\, 2)^T$,\quad
    $(-3,\, 1,\, 3)^T$,\quad
    $(2,\, 10,\, 2)^T$;
\end{enumerate}



## Пример

Совпадает ли линейная оболочка полиномов
$x^3 + 2x$,\quad $x^2 + x + 1$,\quad $x^3 + 5$
с $\mathbb{R}[x,3]$? Обоснуйте ответ.

<!-- src David Lay, 4.4, 31 -->
