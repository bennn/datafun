<!-- Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod
tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam,
quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo
consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum
dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident,
sunt in culpa qui officia deserunt mollit anim id est laborum. -->

\newcommand{\op}[1]{#1^{\ms{op}}}
\newcommand{\D}[1]{\ms{D}\,#1}

# Notation

Give sets $A,B$, posets $P,Q$, and usls (unital semilattices) $M,N$, we use the
following notation:
\begin{center}
  \begin{tabular}{cl}
    $|P|$ & the underlying set of the poset $P$\\
    $P \x_\le Q$ & the poset of pairs of $P$s and $Q$s, ordered pointwise\\
    $P +_\le Q$ & the poset on the disjoint sum of $P$ and $Q$, ordered disjointly\\
    $P \lhd Q$ & the poset on the disjoint sum of $P$ and $Q$ where
    $\ms{in}_1\; x \le \ms{in}_2\; y\ (\forall x \of P,y \of Q)$\\
    $P \mono Q$ & the poset of monotone maps from $P$ to $Q$\\
    $\ms{D}\,A$ & the discrete poset on $A$ (where $x \le y \iff x = y$)\\
    $\FS\;A$ & the usl of finite sets of $A$s, ordered by inclusion
  \end{tabular}
\end{center}

Note that $\ms{D}$ and $|\_|$ are adjoint, and that $|\ms{D}\,A| = A$.

# Language

## Syntax

$$\begin{array}{lrrl}
\text{types} & A,B
&::=& |P| \pipe A \x B \pipe A + B \pipe A \to B\\
\text{poset types} & P,Q
&::=& \ms{D}\;A \pipe P^{\ms{op}}
\pipe P \x Q \pipe P + Q \pipe P \lhd Q \pipe P \to Q\\
&&|\,& \N \pipe \FS\;A\\
\text{lattice types} & M,N
&::=& \N \pipe M \x N \pipe P \to M \pipe \FS\;A\\
\text{expressions} & e
&::=& x \pipe \fn\bind{x} \pipe e_1\;e_2
\pipe (e_1,e_2) \pipe \pi_i\;e\\
&&|\,& \ms{in}_i\; e \pipe \case{e}{x}{e_1}{y}{e_2}\\
&&|\,& |u|\\
\text{monotone exprs} & u
&::=& x \pipe \fn\bind{x} u \pipe u_1\;u_2 \pipe (u_1, u_2) \pipe \pi_i\;u\\
%% &&|\,& e \pipe \ms{let}~|x : P| = u_1 ~\ms{in}~ u_2 \\
&&|\,& \ms{in}_i\; u \pipe \case{u}{x}{u_1}{y}{u_2}\\
&&|\,& \emptyset \pipe u_1 \vee u_2\\
&&|\,& \{u\} \pipe \letin{x}{u_1}{u_2}\\
&&|\,& \fix{x}u\\
&&|\,& u ~\ms{as}~ P
\pipe \ms{disc}\;e ~|~ \ms{let}~\ms{disc}\;x = u_1 ~\ms{in}~ u_2\\
\text{contexts} & \GD &::=& \cdot \pipe \GD, x \of A \\
\text{monotone ctxts} & \GG &::=& \cdot \pipe \GG, x \of P\\
\text{typing judgments} & J &::=& \GD\ent e : A\\
&&|\,& \J{\GD}{\GG}{u}{P}
\end{array}$$

Note that:\vspace{-0.8em}
\begin{itemize}
  \setlength{\itemsep}{0em}
\item Type and poset types are separate, although sharing the overloaded
  notation $\x$, $+$ and $\to$.
\item Lattice types are a syntactic restriction of poset types.
\end{itemize}

## Semantics of types

Types $A$ are interpreted as sets $\den{A}$. Poset types $P$ are interpreted as
posets $\den{P}$. Lattice types are interpreted as usls $\den{M}_L$.

Denotation of types $\den{A}$:
$$\begin{array}{rcl}
  \den{|P|} &=& |\den{P}|\\
  \den{A \x B} &=& \den{A} \x \den{B}\\
  \den{A + B} &=& \den{A} \uplus \den{B}\\
  \den{A \to B} &=& \den{A} \to \den{B}
\end{array}$$

Denotation of posets $\den{P}$:
$$\begin{array}{rcl}
  \den{\ms{D}\,A} &=& \ms{D}\,\den{A}\\
  \den{\N} &=& \pair{\N}{\le}\\
  \den{P \x Q} &=& \den{P} \x_\le \den{Q}\\
  \den{P + Q} &=& \den{P} +_\le \den{Q}\\
  \den{P \lhd Q} &=& \den{P} \lhd \den{Q}\\
  \den{P \to Q} &=& \den{P} \mono \den{Q}\\
  \den{\FS\;A} &=& \FS\;\den{A}
\end{array}$$

## Equality and subtyping

\omitted{I'm not sure I've gotten everything here.}

Nontrivial laws for equality of types $A = B$:
$$
\begin{array}{rcl}
  |P \x Q| &=& |P| \x |Q|\\
  |P + Q| &=& |P| + |Q|\\
  |P \lhd Q| &=& |P| + |Q|\\
  |\ms{D}\,A| &=& A\\
  |\D{A} \to P| &=& A \to |P|\\
\end{array}$$

Nontrivial laws for equality of posets $P = Q$:
$$\begin{array}{rclcl}
  \D{(A \x B)} &=& \D{A} \x \D{B}\\
  \D{(A + B)} &=& \D{A} + \D{B}\\
  \D{(A \to B)} &=& \D{A} \to \D{B}\\
  \op{(\op{P})} &=& P\\
  \op{(P \x Q)} &=& \op{P} \x \op{Q}\\
  \op{(P + Q)} &=& \op{P} + \op{Q}\\
  \op{(P \to Q)} &=& \op{P} \to \op{Q}\\
  \op{P} \to Q &=& P \to \op{Q}
\end{array}$$

Nontrivial laws for subtyping of posets $P \le Q$:
$$\begin{array}{rcl}
  \D{|P|} &\le& P\\
  P + Q &\le& P \lhd Q
\end{array}$$

\textbf{Theorem:} Type equality and subtyping are decidable. \textbf{Proof:}
\omitted{TODO}.

## Typing rules

### Structural rules

These rules are technically unnecessary, as they are (ought to be, no proof yet)
admissible.

$$
\infer[\ms{exchange}]{
  \J{\GD_1,\GD_2}{\GG_1,\GG_2}{e}{A}}{\J{\GD_2,\GD_1}{\GG_2,\GG_1}{e}{A}}
\quad
\infer[\ms{weaken}]{\J{\GD,\GD'}{\GG,\GG'}{e}{A}}{\J{\GD}{\GG}{e}{A}}
$$

As originally formulated, there was an additional structural rule, \ms{forget}:
$$
\infer[\ms{forget}]{\J{\GD,x\of M}{\GG}{e}{N}}{\J{\GD}{\GG,x\of M}{e}{N}}
$$

However, \ms{forget} is not used in any proofs, and is moreover derivable from
weakening and the rules for monotone functions (with a bit of term elaboration):
$$
\infer[\widehat{\ms{app}}]{\J{\GD,x\of M}{\GG}{(\monofn\bind{x} e)\; x}{N}}{
  \infer[\ms{weaken}]{\J{\GD,x\of M}{\GG}{\monofn\bind{x}e}{M \mono N}}{
    \infer[\monofn]{\J{\GD}{\GG}{\monofn\bind{x}e}{M \mono N}}{
      \J{\GD}{\GG,x\of M}{e}{N}}} &
  \infer[\ms{hyp}]{\J{\GD,x\of M}{\GG}{x}{M}}{}
  }
$$

### Other rules

$$
\infer[\ms{hyp}]{\J{\GD}{\GG}{x}{A}}{x\of A \in \GD \cup \GG} \qquad
\infer[\fn]{\J{\GD}{\GG}{\fn\bind{x}{e}}{A \to B}}{
  \J{\GD,x\of A}{\GG}{e}{B}} \qquad
\infer[\ms{app}]{\J{\GD}{\GG}{e_1\;e_2}{B}}{
  \J{\GD}{\GG}{e_1}{A \to B} &
  \J{\GD}{\cdot}{e_2}{B}}
$$\ $$
\infer[\monofn]{\J{\GD}{\GG}{\monofn\bind{x}{e}}{M \mono N}}{
  \J{\GD}{\GG,x \of M}{e}{N}} \qquad
\infer[\widehat{\ms{app}}]{\J{\GD}{\GG}{e_1\;e_2}{N}}{
  \J{\GD}{\GG}{e_1}{M \mono N} &
  \J{\GD}{\GG}{e_2}{M}}
$$\ $$
\infer[(,\!)]{\J{\GD}{\GG}{(e_1, e_2)}{A_1 \x A_2}}{\J{\GD}{\GG}{e_i}{A_i}}
\qquad
\infer[\pi_i]{\J{\GD}{\GG}{\pi_i\; e}{A_i}}{\J{\GD}{\GG}{e}{A_1 \x A_2}}
$$\ $$
\infer[\ms{in}_i]{\J{\GD}{\cdot}{\ms{in}_i\;e}{A_1 + A_2}}{
  \J{\GD}{\cdot}{e}{A_i}} \qquad
\infer[\ms{case}]{\J{\GD}{\GG}{\case{e}{x}{e_1}{y}{e_2}}{C}}{
  \J{\GD}{\cdot}{e}{A + B} &
  \J{\GD,x\of A}{\GG}{e_1}{C} &
  \J{\GD,y\of B}{\GG}{e_2}{C}}
$$\ $$
\infer[\emptyset]{\J{\GD}{\GG}{\emptyset}{M}}{} \qquad
\infer[\vee]{\J{\GD}{\GG}{e_1 \vee e_2}{M}}{\J{\GD}{\GG}{e_i}{M}}
$$\ $$
\infer[\{\}]{\J{\GD}{\GG}{\{e\}}{\FS\;A}}{\J{\GD}{\cdot}{e}{A}} \qquad
\infer[\ms{let}_{\in}]{\J{\GD}{\GG}{\letin{x}{e_1}{e_2}}{M}}{
  \J{\GD}{\GG}{e_1}{\FS\;A} &
  \J{\GD,x\of A}{\GG}{e_2}{M}}
$$\ $$
\infer[\ms{fix}]{\J{\GD}{\GG}{\fix{x}e}{F}}{
  \J{\GD}{\GG,x\of F}{e}{F}}
$$

The \ms{fix} rule is overly permissive in allowing fix-points to be taken at any
lattice type; it needs to be be restricted to some computationally tractable
class of lattice types.



# Denotational semantics

A unital semilattice (usl) is a triple $\triple{A}{\unit}{\vee}$ of a set $A$, a
unit (least element) $\unit : A$, and a join (least upper bound) operator
${\vee} : A \x A \to A$ obeying associativity, commutativity, idempotence, and
identity. Every usl has an associated poset, defined by $(a \le b) \iff (a \vee
b = b)$. Usls may be seen as posets in which every finite set of elements has a
least upper bound; conversely, finite sets (ordered by inclusion) are the free
usl.

We write $\unit$, $\vee$, and $\le$ for the unit, join, and partial-order
of an unspecified usl, or subscript them to specify a particular usl.

We consider only usls in which $\unit$ and $\vee$ are computable. However,
equality $=$ and thus ordering $\le$ may not always be decidable.

Let \ms{Set} be the category of sets and functions and \ms{USL} be the category
of usls and monotone functions.

Given sets $A,B$ and usls $M$, $N$ we use the following notation:
\begin{center}\begin{tabular}{cl}
    \one & one-element set, $\{\triv\}$\\
    $M \mono N$ & set of monotone functions from $M$ to $N$\\
    $\FS\;A$ & set of finite subsets of $A$\\
    $|M|$ & underlying set of $M$\\
    $\one_L$ & trivial one-element usl\\
    $M \x_L N$ & pointwise usl on pairs of $M$s and $N$s\\
    $A \to_L M$ & pointwise usl of functions from $A$ to $M$\\
    $M \mono_L N$ & pointwise usl of monotone functions from $M$ to $N$\\
    $\FS_L\;A$ & usl of finite subsets of $A$ under inclusion\\
\end{tabular}\end{center}

## Semantics of types and contexts

We define a semantics of types and contexts with the following signaturee:
$$\begin{array}{ccc}
  \den{A}, \den{\GD} &\in& \ms{Set}_0\\
  \den{M}_L, \den{\GG}_L &\in& \ms{USL}_0\\
  |\den{M}_L| &=& \den{M}
\end{array}$$

We define $\den{A}$ as follows:
$$\begin{array}{lcl}
  \den{\N} &=& \N\\
  \den{A \to B} &=& \den{A} \to \den{B}\\
  \den{A \x B} &=& \den{A} \x \den{B}\\
  \den{A + B} &=& \den{A} \uplus \den{B}\\
  %% \den{\FS\;A} &=& \{x ~|~ x \subseteq \den{A} \wedge x\text{ is finite}\}\\
  \den{\FS\;A} &=& \FS\;\den{A}\\
  \den{M \mono N} &=& \den{M}_L \mono \den{N}_L
\end{array}$$

We define $\den{M}_L$ as follows:
$$\begin{array}{lcl}
  \den{\N}_L &=& \triple{\N}{0}{\ms{max}}\\
  \den{A \to M}_L &=& \den{A} \to_L \den{M}_L\\
  %% &=& \triple{\den{A \to M}}{\fn\bind{x}\unit}{%
  %%   \fn\bind{\tuple{f,g}} \fn\bind{x} f(x) \vee g(x)}\\
  \den{M \x N}_L &=& \den{A}_L \x_L \den{B}_L\\
  %% \den{M \x N}_L &=& \triple{\den{A \x B}}{\tuple{\unit,\unit}}{%
  %%   \fn\bind{\tuple{\tuple{a,x},\tuple{b,y}}} \pair{a \vee b}{x \vee y}}\\
  %% \den{\FS\;A}_L &=& \triple{\den{\FS\;A}}{\emptyset}{\cup}\\
  \den{\FS\;A}_L &=& \FS_L\;\den{A}\\
  \den{M \mono N}_L &=& \den{M}_L \mono_L \den{N}_L\\
  %% &=& \triple{\den{M}_L \mono \den{N}_L}{\fn\bind{x}\unit}{%
  %%   \fn\bind{\tuple{f,g}}\fn\bind{x} f(x) \vee g(x)}
\end{array}$$

We extend these to contexts $\den{\GD}$, $\den{\GG}_L$ as follows:
$$\begin{array}{lcl}
  \den{\cdot} &=& \one\\
  \den{\GD,A} &=& \den{\GD} \x \den{A}\\
  \den{\cdot}_L &=& \one_L\\
  \den{\GG,M}_L &=& \den{\GG}_L \x_L \den{M}_L
\end{array}$$

## Semantics of type derivations

We define a semantics on type derivations $J$ with the following signature:
$$\begin{array}{lcl}
  \den{\J{\GD}{\GG}{e}{M}} &\in& \den{\GD} \to \den{\GG}_L \mono \den{M}_L\\
  \den{\J{\GD}{\cdot}{e}{A}} &\in& \den{\GD} \to \one \to \den{A}\\
\end{array}$$

The above signatures overlap in the case of type derivations of the form
$\J{\GD}{\cdot}{e}{M}$. However, this is not a problem, since $(\den{\cdot}_L
\mono \den{M}_L) = (\one_L \mono \den{M}_L) = (\one \to \den{M})$ as all
functions out of \one{} are monotone.

\newcommand{\fux}[2]{\Den{\vcenter{\infer{#1}{#2}}}}
\newcommand{\dg}{\;\delta\;\gamma}

$$
\begin{array}{rcll}
  \textbf{Derivation} && \textbf{Denotes}
  & \textbf{Monotone in }\gamma
  \vspace{.4em}\\
  \fux{\J{x_1\of A_1, ..., x_n\of A_N}{\GG}{x_i}{A_i}}{\phantom{.}}\dg
  &=& \pi_i\;\delta & \text{constant in }\gamma
  \vspace{.8em}\\
  \fux{\J{\GD}{x_1\of M_1, ..., x_n\of M_n}{x_i}{M_i}}{\phantom{.}}\dg
  &=& \pi_i\;\gamma & \pi_i\text{ monotone}
  \vspace{.8em}\\
  \fux{\J{\GD}{\GG}{\emptyset}{M}}{\phantom{.}}\dg
  %% \den{\emptyset : M}\dg
  &=& \unit_{\den{M}_L} & \text{constant in }\gamma
  \vspace{.8em}\\
  \fux{\J{\GD}{\GG}{e_1 \vee e_2}{M}}{
    \J{\GD}{\GG}{e_1}{M} &
    \J{\GD}{\GG}{e_2}{M}}\dg
  %% \den{e_1 \vee e_2 : M}\dg
  &=& \den{e_1}\dg \vee_{\den{M}_L} \den{e_2}\dg
  & \text{$\vee$ monotone, IHs}
  \vspace{.8em}\\
  \fux{\J{\GD}{\GG}{\{e\}}{\FS\;A}}{\J{\GD}{\cdot}{e}{A}}\dg
  &=& \{\den{e}\;\delta\;\triv\} & \text{constant in }\gamma
  \vspace{.8em}\\
  \fux{\J{\GD}{\GG}{\letin{x}{e_1}{e_2}}{M}}{
    \J{\GD}{\GG}{e_1}{\FS\;A} &
    \J{\GD,x\of A}{\GG}{e_2}{M}}\dg
  &=& \displaystyle\bigvee_{x \,\in\, \den{e_1}\,\delta\,\gamma}
  \den{e_2}\;\tuple{\delta,x}\;\gamma
  & \text{(see below)}
  \vspace{.8em}\\
  \fux{\J{\GD}{\GG}{\fn\bind{x} e}{A \to B}}{
    \J{\GD,x\of A}{\GG}{e}{B}}\dg
  &=& x \mapsto \den{e}\;\tuple{\delta,x}\;\gamma
  & \den{e}\text{ monotone}
  \vspace{.8em}\\
  \fux{\J{\GD}{\GG}{e_1\;e_2}{B}}{
    \J{\GD}{\GG}{e_1}{A \to B} &
    \J{\GD}{\cdot}{e_2}{A}} \dg
  &=& \den{e_1}\dg\;(\den{e_2}\;\delta\;\triv)
  & \text{\omitted{TODO}}
  \vspace{.8em}\\
  \fux{\J{\GD}{\GG}{\monofn\bind{x} e}{M \mono N}}{
    \J{\GD}{\GG,x\of M}{e}{N}}\dg
  &=& x \mapsto \den{e} \;\delta \;\tuple{\gamma,x}
  & \den{e}\text{ monotone}\\
  \vspace{.8em}\\
  \fux{\J{\GD}{\GG}{e_1\;e_2}{N}}{
    \J{\GD}{\GG}{e_1}{M \mono N} &
    \J{\GD}{\GG}{e_2}{N}} \dg
  &=& \den{e_1}\dg\;(\den{e_2}\dg)
  & \den{e_i}\text{ monotone}
  \vspace{.8em}\\
  \fux{\J{\GD}{\cdot}{\ms{in}_i\;e}{A_1 + A_2}}{
    \J{\GD}{\cdot}{e}{A_i}}\;\delta\;\triv
  &=& \ms{in}_i\;(\den{e} \;\delta\;\triv)
  & \text{(meaningless)}
  \vspace{.8em}\\
  \fux{\J{\GD}{\GG}{\case{e}{x}{e_1}{x}{e_2}}{B}}{
    \J{\GD}{\cdot}{e}{A_1 + A_2} &
    \J{\GD,x\of A_i}{\GG}{e_i}{B}}
  \dg
  &=&
  \begin{cases}
    \den{e_1}\;\pair{\delta}{x}\;\gamma
    &\text{if }\den{e_2}\;\delta\;\triv = \ms{in}_1\;x\\
    \den{e_2}\;\pair{\delta}{x}\;\gamma
    &\text{if }\den{e_2}\;\delta\;\triv = \ms{in}_2\;x\\
  \end{cases}
  & \den{e_i}\text{ monotone}
  \vspace{.8em}\\
  \fux{\J{\GD}{\GG}{(e_1, e_2)}{A_1 \x A_2}}{
    \J{\GD}{\GG}{e_i}{A_i}}\dg
  &=& \pair{e_1\dg}{e_2\dg} & \den{e_i}\text{ monotone}
  \vspace{.8em}\\
  \fux{\J{\GD}{\GG}{\pi_i\;e}{A_i}}{
    \J{\GD}{\GG}{e}{A_1 + A_2}}\dg
  &=& \pi_i\;(\den{e}\dg) & \pi_i,\,\den{e}\text{ monotone}
  \vspace{.8em}\\
  \fux{\J{\GD}{\GG}{\fix{x}e}{F}}{
    \J{\GD}{\GG,x\of F}{e}{F}}\dg
  &=& \ms{fix}_{\den{F}_L}\;(\fn\bind{x} \den{e}\;\pair{\delta}{x}\;\gamma)
  & \text{\omitted{TODO}}
\end{array}
$$

\omitted{TODO: show denotation of $\ms{let}_\in$ is monotone in $\gamma$}

\omitted{TODO: show denotation of $\fix{x} e$ is monotone in $\gamma$}

Note that the denotation of $\fix{x} e$ being well-defined relies on the
following lemma:

\textbf{Lemma:} The denotation $\den{F}_L$ of a finite lattice type $F$ is a
finite usl. \textbf{Proof:} \omitted{Omitted}.

From this it follows immediately (\omitted{TODO: reference some proof of this
  well-known fact}) that it is a complete join-semilattice, and therefore a
complete lattice, and therefore has a least fix-point (by Knaster-Tarski).



# Proofs

## Admissibility of {\ms{exchange},\ms{weaken}}

\textcolor{red}{TODO}

## Syntactic substitution

Note that whenever two variables are given distinct names $x, y$ it is assumed
$x \ne y$ unless mentioned otherwise.

We could choose to define two substitution operators, one for unrestricted
substitution and the other for monotone substitution, but they coincide on
properly-typed arguments (see substitution theorems below for what I mean by
properly-typed arguments), so we don't bother.

We define substitution $\sub{e_1/x} e_2$, by induction on $e_2$:

$$
\begin{array}{rcl}
  \sub{e/x} x &=& e\\
  \sub{e/x} y &=& y\\
  \sub{e/x}(\fn\bind{y} e') &=& \fn\bind{y} \sub{e/x} e'\\
  \sub{e/x}(\monofn\bind{y} e') &=& \monofn\bind{y} \sub{e/x} e'\\
  \sub{e/x}(e_1\;e_2) &=& (\sub{e/x} e_1)\;(\sub{e/x}e_2)\\
  \sub{e/x}(e_1, e_2) &=& (\sub{e/x}e_1, \sub{e/x}e_2)\\
  \sub{e/x}(\pi_i\; e') &=& \pi_i\;(\sub{e/x} e')\\
  \sub{e/x}(\ms{in}_i\;e') &=& \ms{in}_i\;(\sub{e/x}e')\\
  \sub{e/x}(\case{e'}{y}{e_1}{z}{e_2})
  &=& \case{\sub{e/x} e'}{y}{\sub{e/x}e_1}{z}{\sub{e/x}e_2}\\
  \sub{e/x} \emptyset &=& \emptyset\\
  \sub{e/x}(e_1 \vee e_2) &=& (\sub{e/x}e_1) \vee (\sub{e/x} e_2)\\
  \sub{e/x}\{e'\} &=& \{\sub{e/x}e'\}\\
  \sub{e/x}(\letin{y}{e_1}{e_2}) &=& \letin{y}{\sub{e/x}e_1}{\sub{e/x}e_2}\\
  \sub{e/x}(\fix{y} e') &=& \fix{y} \sub{e/x} e'
\end{array}
$$

\textbf{Lemma, useless substitution:} If $\J{\GD}{\GG}{e}{A}$ and $x \not\in
\GD\cup\GG$, then $\sub{e'/x}e = e$. \textbf{Proof:} \omitted{Omitted}.

<!-- TODO: theorem numbering. what package provides \begin{theorem} again? -->


\textbf{Theorem 1.1, substitution for unrestricted variables:} If
$\J{\GD}{\cdot}{e}{A}$ and $\J{\GD,x\of A}{\GG}{e'}{B}$ then
$\J{\GD}{\GG}{\sub{e/x}{e'}}{B}$.

\textbf{Proof:} By induction on $\J{\GD,x\of A}{\GG}{e'}{B}$, assuming in each
case that $\J{\GD}{\cdot}{e}{A}$:

\begin{quote}
  \begin{description}
  %% \item[Case \(\infer{\J{\GD,x\of A}{\GG}{x}{A}}{x\of A \in \GD\cup\GG}\):]
  %%   By assumption, $\J{\GD}{\GG}{e}{A}$
  \item[Case \ms{hyp}, $x \ne y$:] Given \[
    \infer[\ms{hyp}]{\J{\GD,x\of A}{\GG}{y}{B}}{
      y\of B \in (\GD,x\of A)\cup\GG}
    \]

    Since $x \ne y$, evidently $y \of B \in \GD \cup \GG$, thus:
    \[\infer[\ms{hyp}]{\J{\GD}{\GG}{y}{B}}{y\of B \in \GD\cup\GG}\]

  \item[Case \ms{hyp}, $x = y$:] Given \[
    \infer[\ms{hyp}]{\J{\GD,x\of A}{\GG}{x}{A}}{
      x\of A \in (\GD,x\of A)\cup\GG}\]

    By weakening our assumption we have $\J{\GD}{\GG}{e}{A}$, which suffices.

  \item[Case $\fn$]: Given \[
    \infer[\fn]{\J{\GD,x\of A}{\GG}{\fn\bind{y} e'}{B \to C}}{
      \J{\GD,x\of A,y\of B}{\GG}{e'}{C}}
    \]

    By our IH, exchange, and weakening, we have $\J{\GD,y :
      B}{\GG}{\sub{e/x}e'}{C}$. Thus:
    \[
    \infer{\J{\GD}{\GG}{\fn\bind{y} \sub{e/x} e'}{B \to C}}{
      \J{\GD,y : B}{\GG}{\sub{e/x}e'}{C}}
    \]

  \item[Case $\monofn$]: Given \[
    \infer[\monofn]{\J{\GD,x\of A}{\GG}{\monofn\bind{y} e'}{M \mono N}}{
      \J{\GD,x\of A}{\GG,y \of M}{e'}{N}}
    \]

    By our IH, we have $\J{\GD}{\GG,y \of M}{\sub{e/x}e'}{N}$. Thus:
    \[
    \infer[\monofn]{\J{\GD}{\GG}{\monofn\bind{y} \sub{e/x}e'}{M \mono N}}{
      \J{\GD}{\GG,y\of M}{\sub{e/x} e'}{N}
      }
    \]

  \item[Case $\ms{app}$:] Given \[
    \infer[\ms{app}]{\J{\GD,x\of A}{\GG}{e_1\;e_2}{C}}{
      \J{\GD,x\of A}{\GG}{e_1}{B \to C} &
      \J{\GD,x\of A}{\cdot}{e_2}{B}}
    \]

    By our IHs, we have $\J{\GD}{\GG}{\sub{e/x} e_1}{B\to C}$ and
    $\J{\GD}{\cdot}{\sub{e/x}e_2}{B}$. Thus: \[
    \infer[\ms{app}]{\J{\GD}{\GG}{(\sub{e/x} e_1)\;(\sub{e/x} e_2)}{C}}{
        \J{\GD}{\GG}{\sub{e/x} e_1}{B \to C} &
        \J{\GD}{\cdot}{\sub{e/x} e_2}{B}}
    \]

  \item[Case $\widehat{\ms{app}}$:] Given \[
    \infer[\widehat{\ms{app}}]{\J{\GD,x\of A}{\GG}{e_1\;e_2}{N}}{
      \J{\GD,x\of A}{\GG}{e_1}{M \mono N} &
      \J{\GD,x\of A}{\GG}{e_2}{N}}
    \]

    By our IHs, we have $\J{\GD}{\GG}{\sub{e/x} e_1}{M\to N}$ and
    $\J{\GD}{\GG}{\sub{e/x}e_2}{M}$. Thus: \[
    \infer[\widehat{\ms{app}}]{
      \J{\GD}{\GG}{(\sub{e/x} e_1)\;(\sub{e/x} e_2)}{N}
    }{
        \J{\GD}{\GG}{\sub{e/x} e_1}{M \mono N} &
        \J{\GD}{\GG}{\sub{e/x} e_2}{M}}
    \]

  \item[Case \ms{case}:] Given \[
    \infer{
      \J{\GD,x\of A}{\GG}{\case{e'}{y}{e_1}{z}{e_2}}{D}
    }{
      \J{\GD,x\of A}{\cdot}{e'}{B + C} &
      \J{\GD,x\of A,y\of B}{\GG}{e_1}{D} &
      \J{\GD,x\of A,z\of C}{\GG}{e_2}{D}
    }
    \]

    By our IHs, exchange, and weakening, we have:
    \begin{itemize}
    \item $\J{\GD}{\cdot}{\sub{e/x} e'}{B + C}$,
    \item $\J{\GD,y\of B}{\GG}{\sub{e/x}e_1}{D}$, and
    \item $\J{\GD,z \of C}{\GG}{\sub{e/x} e_2}{D}$.
    \end{itemize}
    Thus:
    \[
    \infer{
      \J{\GD}{\GG}{\case{\sub{e/x}e'}{y}{\sub{e/x}e_1}{z}{\sub{e/x}e_2}}{D}
    }{
      \J{\GD}{\cdot}{\sub{e/x}e'}{B + C} &
      \J{\GD,y\of B}{\GG}{\sub{e/x}e_1}{D} &
      \J{\GD,z\of C}{\GG}{\sub{e/x}e_2}{D}
    }
    \]

  \item[Case $\{\}$:] Given \[
    \infer[\{\}]{\J{\GD,x\of A}{\GG}{\{e'\}}{\FS\;B}}{
      \J{\GD,x\of A}{\cdot}{e'}{B}}
    \]

    By IH we have $\J{\GD}{\cdot}{\sub{e/x} e'}{B}$, thus:\[
    \infer[\{\}]{\J{\GD}{\GG}{\{\sub{e/x} e'\}}{\FS\;B}}{
      \J{\GD}{\cdot}{\sub{e/x} e'}{B}}
    \]

  \item[Case $\ms{let}_{\in}$:] Given \[
    \infer[\ms{let}_{\in}]{\J{\GD,x\of A}{\GG}{\letin{y}{e_1}{e_2}}{M}}{
      \J{\GD,x\of A}{\GG}{e_1}{\FS\;B} &
      \J{\GD,x\of A,y\of B}{\GG}{e_2}{M}}\]

    By our IHs, exchange, and weakening, we have
    $\J{\GD}{\GG}{\sub{e/x}e_1}{\FS\;B}$ and $\J{\GD,y\of B}{\GG}{\sub{e/x}
      e_2}{M}$. Thus:
    \[
    \infer[\ms{let}_{\in}]{
      \J{\GD}{\GG}{\letin{y}{\sub{e/x}e_1}{\sub{e/x}e_2}}{M}
    }{
      \J{\GD}{\GG}{\sub{e/x} e_1}{\FS\;B} &
      \J{\GD,y\of B}{\GG}{\sub{e/x} e_2}{M}
    }
    \]

  \item[Case $\ms{fix}$:] Given \[
    \infer[\ms{fix}]{\J{\GD,x\of A}{\GG}{\fix{y} e'}{M}}{
      \J{\GD,x\of A}{\GG,y \of M}{e'}{M}}
    \]

    By our IH we have $\J{\GD}{\GG,y\of M}{\sub{e/x} e'}{M}$. Thus: \[
    \infer[\ms{fix}]{\J{\GD}{\GG}{\fix{y} \sub{e/x} e'}{M}}{
      \J{\GD}{\GG,y\of M}{\sub{e/x} e'}{M}
    }\]

  \item[\omitted{Omitted cases:}] $(,\!)$, $\pi_i$, $\ms{in}_i$,
    $\emptyset$, and ${\vee}$ are trivial.

  \end{description}
\end{quote}


\textbf{Theorem 1.2, substitution for monotone variables:} If
$\J{\GD}{\GG}{e}{M}$ and $\J{\GD}{\GG,x \of M}{e'}{N}$ then
$\J{\GD}{\GG}{\sub{e/x}{e'}}{N}$.

\textbf{Proof:} By induction on $\J{\GD}{\GG,x \of M}{e'}{N}$, assuming
$\J{\GD}{\GG}{e}{M}$ in each case:

\begin{quote}
  \begin{description}
  \item[Case \ms{hyp}, $x \ne y$:] Given \[
    \infer{\J{\GD}{\GG,x\of M}{y}{N}}{y\of N \in \GD\cup(\GG,x\of M)}
    \]

    Since $x \ne y$, evidently $y\of N \in \GD \cup \GG$. Thus:\[
    \infer{\J{\GD}{\GG}{y}{N}}{y\of N \in \GD\cup\GG}
    \]

  \item[Case \ms{hyp}, $x = y$:] Given \[
    \infer{\J{\GD}{\GG,x\of M}{x}{M}}{x\of M \in \GD\cup\GG}
    \]

    By assumption, $\J{\GD}{\GG}{e}{M}$, which suffices.

  \item[Case $\fn$]: Given \[
    \infer{\J{\GD}{\GG,x\of M}{\fn\bind{y}{e'}}{A \to N}}{
      \J{\GD,y\of A}{\GG,x\of M}{e'}{N}}\]

    By our IH and weakening, $\J{\GD,y:A}{\GG}{\sub{e/x} e'}{N}$. Thus: \[
    \infer{\J{\GD}{\GG}{\fn\bind{y} \sub{e/x} e'}{A \to N}}{
      \J{\GD,y\of A}{\GG}{\sub{e/x} e'}{N}}
    \]

  \item[Case $\monofn$]: Given \[
    \infer{\J{\GD}{\GG,x \of M}{\monofn\bind{y} e'}{N \mono O}}{
      \J{\GD}{\GG,x \of M, y \of N}{e'}{O}}
    \]

    By our IH, exchange, and weakening, we have $\J{\GD}{\GG,y\of N}{\sub{e/x}
      e'}{O}$. Thus:
    \[
    \infer{\J{\GD}{\GG}{\monofn\bind{y} \sub{e/x} e'}{N \mono O}}{
      \J{\GD}{\GG,y\of N}{\sub{e/x} e'}{O}}
    \]

  \item[Case $\ms{app}$:] Given \[
    \infer{\J{\GD}{\GG,x \of M}{e_1\;e_2}{N}}{
      \J{\GD}{\GG,x\of M}{e_1}{A \to N} &
      \J{\GD}{\cdot}{e_2}{A}}
    \]

    By our IH we have $\J{\GD}{\GG}{\sub{e/x} e_1}{A \to N}$. Since $x$ does not
    occur free in $e_2$, $\sub{e/x} e_2 = e_2$. Thus, this suffices:
    \[
    \infer{\J{\GD}{\GG}{(\sub{e/x} e_1)\;e_2}{N}}{
      \J{\GD}{\GG}{\sub{e/x} e_1}{A \to N} &
      \J{\GD}{\cdot}{e_2}{A}}
    \]

  \item[Case $\widehat{\ms{app}}$:] Given \[
    \infer{\J{\GD}{\GG,x \of M}{e_1\;e_2}{O}}{
      \J{\GD}{\GG,x \of M}{e_1}{N \mono O} &
      \J{\GD}{\GG,x \of M}{e_2}{N}}
    \]

    By our IHs, we have $\J{\GD}{\GG}{\sub{e/x}e_1}{N \mono O}$ and
    $\J{\GD}{\GG}{\sub{e/x}e_2}{N}$. Thus:
    \[
    \infer{\J{\GD}{\GG}{(\sub{e/x} e_1)\;(\sub{e/x} e_2)}{O}}{
      \J{\GD}{\GG}{\sub{e/x} e_1}{N \mono O} &
      \J{\GD}{\GG}{\sub{e/x} e_2}{N}}
    \]

  \item[Case \ms{case}:] Given \[
    \infer{\J{\GD}{\GG,x\of M}{\case{e'}{y}{e_1}{z}{e_2}}{N}}{
      \J{\GD}{\cdot}{e'}{A + B} &
      \J{\GD,y \of A}{\GG,x\of M}{e_1}{N} &
      \J{\GD,z \of B}{\GG,x\of M}{e_2}{N}}
    \]

    Since $x$ does not occur free in $e'$, $\sub{e/x}e' = e'$. By our IHs and
    weakening, we have $\J{\GD,y\of A}{\GG}{\sub{e/x} e_1}{N}$ and $\J{\GD,z\of
      B}{\GG}{\sub{e/x}e_2}{N}$. Thus, this suffices:
    \[
    \infer{\J{\GD}{\GG}{\case{e'}{y}{\sub{e/x}e_1}{z}{\sub{e/x}e_2}}{N}}{
      \J{\GD}{\cdot}{e'}{A+B} &
      \J{\GD,y\of A}{\GG}{\sub{e/x} e_1}{N} &
      \J{\GD,z\of B}{\GG}{\sub{e/x} e_2}{N}}
    \]

  \item[Case $\{\}$:] Given \[
    \infer{\J{\GD}{\GG,x\of M}{\{e'\}}{\FS\;A}}{
      \J{\GD}{\cdot}{e'}{A}}
    \]

    Since $x$ does not occur free in $e'$, $\sub{e/x} e' = e'$. Thus, this
    suffices:
    \[
    \infer{\J{\GD}{\GG}{\{e'\}}{\FS\;A}}{\J{\GD}{\cdot}{e'}{A}}
    \]

  \item[Case $\ms{let}_{\in}$:] Given \[
    \infer{\J{\GD}{\GG,x\of M}{\letin{y}{e_1}{e_2}}{N}}{
      \J{\GD}{\GG,x\of M}{e_1}{\FS\;A} &
      \J{\GD,y\of A}{\GG,x\of M}{e_2}{N}}
    \]

    By our IHs and weakening, we have $\J{\GD}{\GG}{\sub{e/x} e_1}{\FS\;A}$
    and $\J{\GD,y\of A}{\GG}{\sub{e/x} e_2}{N}$. Thus:
    \[
    \infer{\J{\GD}{\GG}{\letin{y}{\sub{e/x}e_1}{\sub{e/x}e_2}}{N}}{
      \J{\GD}{\GG}{\sub{e/x} e_1}{\FS\;A} &
      \J{\GD,y\of A}{\GG}{\sub{e/x} e_2}{N}}
    \]

  \item[Case $\ms{fix}$:] Given \[
    \infer{\J{\GD}{\GG,x\of M}{\fix{y} e'}{N}}{
      \J{\GD}{\GG,x\of M,y\of N}{e'}{N}}
    \]

    By our IH and weakening, we have $\J{\GD}{\GG,y \of N}{\sub{e/x} e'}{N}$.
    Thus: \[
    \infer{\J{\GD}{\GG}{\fix{y} \sub{e/x} e'}{N}}{
      \J{\GD}{\GG,y\of N}{\sub{e/x} e'}{N}}
    \]

  \item[\omitted{Omitted cases:}] $(,\!)$, $\pi_i$, $\ms{in}_i$,
    $\emptyset$, and ${\vee}$ are trivial.
  \end{description}
\end{quote}