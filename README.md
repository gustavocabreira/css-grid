# CSS Grid
CSS Grid é um sistema bidimensional, ou seja, ele consegue controlar linhas e colunas no seu site. Basicamente, você consegue trabalhar com o CSS Grid aplicando regras de CSS para um elemento pai (parent - chamado de container) e nos elementos filhos.

## Container

O container é a div pai que irá armazenar os itens do grid. Nele, colocaremos o display como grid.
```
<div class="container">
    <div class="item">ITEM 1</div>
    <div class="item">ITEM 2</div>
    <div class="item">ITEM 3</div>
    <div class="item">ITEM 4</div>
    <div class="item">ITEM 5</div>
</div>
```
```
.container {
    display: grid;
}
```
Todos os filhos diretos que estão dentro da div do container, agora, são identificados como itens do grid. Por enquanto, não se deve notar nenhuma alteração dentro do visual da página pois ainda não aplicamos regras para definirmos os tamanhos e posições de linhas e colunas.

### Inspecionando elementos
Se você utilizar o inspecionador de elementos do chrome e passar o mouse por cima do html da div do container, você verá que, agora, ela possui uma borda invisível, indicando o grid dela.

Essa é uma forma de verificar a posição dos seus itens e espaçamento do grid da maneira mais fácil. Você pode, também, adicionar background-colors nas linhas, colunas e células (itens) do grid.

# Linhas e colunas

## Colunas
Podemos definir o tamanho e quantidade das colunas da seguinte forma:
```
.container {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
}
```
Utilizando a unidade de medida *fr* (fração), dizemos que nosso grid terá três colunas e, seus tamanhos, serão de 100% do tamanho do container, divido pela quantidade de medidas (fr, pxs, etc.);

Podemos, também, deixar o tamanho de uma coluna fixa em píxeis e as outras duas variam de acordo com a largura do container. Por exemplo:
```
.container {
    display: grid;
    grid-template-columns: 1fr 150px 1fr;
}
```

## Linhas
As linhas são definidas da mesma forma do que as colunas. A unica diferença é o comando que utilizaremos para definir a propriedade de tamanho.
```
.container {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    grid-template-rows: 1fr 1fr;
}
```
No exemplo acima, definimos que nosso grid, agora, possui 3 colunas e duas linhas. Agora, passaremos a posicionar os elementos dentro do nosso grid.

### Quando temos o mesmo tamanho para todos as colunas/linhas
Quando o tamanho das linhas ou colunas forem iguais, podemos utilizar a seguinte propriedade:
```
.container {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-template-rows: repeat(2, 1fr);
}
```

# Posicionamento

## Posicionamento do grid/itens
Para posicionar o grid e os itens, temos seis comandos disponíveis:
- justify-items
- align-items
- justify-content
- align-content
- justify-self
- align-self

Em todos esses comandos, podemos definir como propriedades:
- *start*: alinha o elemento no começo do container;
- *end*: alinha o elemento no fim do container;
- *center*: alinha o elemento no centro do container;
- *stretch*: redimensiona o elemento para garantir que preencherá o tamanho total do grid do container;
- *space-around*: define um espaçamento igual entre cada item do grid, com metade desse espaçamento no fim;
- *space-between*: define um espaçamento igual entre cada item do grid, sem espaço no fim;
- *space-evenly*: define um espaçamento igual entre cada item do grid, incluindo no fim;

Vamos, no entanto, separar isso em dois blocos de aprendizado: [justify e align] e [items, content, self].

### Justify
No prefixo justify, alteramos o alinhamento no eixo x (horizontal), da esquerda para a direita.

### Align
No prefixo justify, alteramos o alinhamento no eixo y (vertical), de cima para baixo.

# Itens
Para explicar como funciona a delimitação de espaçamento de itens no grid, preciso, primeiro, explicar o que são linhas virtuais.

### Linhas virtuais
Linhas virtuais são as linhas que delimitam o onde começam e terminam as linhas do seu grid.

#### 3 linhas
Um grid com três linhas terá, na verdade, quatro linhas virtuais (representado pelas linhas pontilhadas). Contamos, também, a primeira linha do grid como uma linha. Ou seja, temos: 
```
----------------
linha do grid
----------------
linha do grid
----------------
linha do grid
----------------
```

Agora, sim, podemos continuar com a parte de posicionar os itens dentro do grid.

No exemplo que já temos, temos um grid com três colunas, duas linhas e cinco itens. A ideia principal é criar da seguinte forma:
```
---------------------------------
|               |               |
|               |               |
|               |               |
|               |               |
---------------------------------
|          |         |          |
|          |         |          |
|          |         |          |
----------------------------------
```
Para desenharmos o layout da seguinte forma, precisamos definir que o primeiro item comece na primeira linha virtual da coluna e termine na terceira linha virtual dela. Também precisamos dizer que ele deverá começar na primeira linha virtual da linha do grid e terminar na segunda linha virtual do grid.
```
.container > div:nth-child(1) {
    grid-column-start: 1;
    grid-column-end: 3;
    grid-row-start: 1;
    grid-row-end: 2;
    justify-self: center;
    align-self: center;
}
```
Precisamos, agora, definir o segundo item. Sua coluna começará na segunda linha virtual do grid e terminará na quinta linha virtual do grid.
```
.container > div:nth-child(2) {
    grid-column-start: 2;
    grid-column-end: 4;
    grid-row-start: 1;
    grid-row-end: 2;
    justify-self: center;
    align-self: center;
}
```
Agora, automaticamente, o resto se dividirá no grid. Precisamos, apenas, alinhar no centro.
```
.container > div:nth-child(n + 2) {
    justify-self: center;
    align-self: center;
}
```
