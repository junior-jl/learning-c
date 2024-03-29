# The C Programming Language - Ritchie and Kernighan (2nd edition)
## Chapter 1 - A Tutorial Introduction

### Função main

<div align="justify">
  


Todo programa em C precisa de uma função **main**. A execução do programa começa nesta função. **main** geralmente chama funções previamente escritas pelo usuário ou de bibliotecas. 
Em vários programas escritos em C, a primeira linha será **#include <stdio.h>**, que diz ao compilador para incluir as informações da biblioteca "standard input/output". O programa inicial no
estudo das linguagens de programação geralmente é escrever "Hello, world", em C, tem-se:

```c
#include <stdio.h>

main(){
  printf("Hello, world\n");
}
```

### Funções, parâmetros e declarações

A fim de comunicar dados entre funções, pode-se fornecer uma lista de **argumentos (parâmetros)**. Essa lista é escrita dentro dos parênteses após o nome da função. 
Ainda, entre as chaves, estão os _statements_ (declarações).

Dessa forma, funções são chamadas nomeando-as e em seguida listando seus parâmetros entre parênteses. Pode-se observar no exemplo anterior a função **printf** foi nomeada e
após isso, o argumento "Hello, world\n". 

**printf** é uma função de biblioteca que imprime saída, neste caso, a sequência entre aspas duplas, chamada _character string_ ou _string constant_. 

#### Sequências de escape

O \n é uma **sequência de escape**, isto é, uma sequência de caracteres (dentro de uma _string_) que representa outro caractere ou sequência de caracteres. Abaixo, tem-se uma lista de algumas sequências de escape utilizadas em C (todas iniciam com o \).

Sequência | Representação
------------ | -------------
\n | newline
\b | backspace
\t | horizontal tab
\v | vertical tab
\" | double quotation mark (")

### Comentários

Tudo que estiver entre /* e */ é ignorado pelo compilador (ou após // numa linha única).

### Variáveis

Em C, todas as variáveis devem ser declaradas antes de serem usadas. Uma declaração consiste no tipo e nome da variável, por exemplo,

```c
int variavel1, variavel2;
```

O tipo **int** significa que as variáveis listadas são inteiros, em contraste com **float**, por exemplo, que significa ponto flutuante (números que podem ter parte fracionária).

A faixa de valores que **int** e **float** podem assumir depende da máquina utilizada. É bastante comum **ints** de 16-bits (valores entre -32768 e +32767) ou 32-bits.
Um número **float** geralmente é uma quantidade de 32-bits com pelo menos seis dígitos significativos, com magnitude variando entre 10<sup>-38</sup> e 10<sup>38</sup>.

Em C, ainda existem outros tipos básicos de dados além de **int** e **float**, incluindo:
Tipo | Significado
------------ | -------------
char | character (a single byte)
short | short integer
long | long integer
double | double-precision floating point

Da mesma forma, o tamanho desses tipos depende da máquina na qual o programa está sendo executado. Ainda há _arrays_ (vetores), _structures_ e _unions_ destes tipos básicos, ponteiros para eles, e funções que os retornam.

O código abaixo imprime uma tabela de valores de temperatura Fahrenheit (de 0 a 300, variando de 20 em 20) e seu equivalente em Celsius.

```c
#include <stdio.h>
main(){
    int fahr, celsius;
    int inferior, superior, passo;
    inferior = 0;
    passo = 20;
    superior = 300;
    fahr = inferior;
    while (fahr <= superior){
        celsius = 5 * (fahr - 32) / 9;
        printf("%d\t%d\n", fahr, celsius);
        fahr = fahr + passo;
    }
}
```

Esse código resulta em: 

![image](https://user-images.githubusercontent.com/69206952/136628685-e96cc717-6cdb-4f14-af9a-6e2fb1381145.png)

O primeiro passo após a declaração de variáveis é passar a estas um valor (fazer o seu _assignment_), que é o que está sendo feito em:

```c
inferior = 0;
passo = 20;
superior = 300;
fahr = inferior;
```

_Statements_ individuais são terminados por ";" (_semicolon_ - ponto e vírgula).

### Laço de repetição _while_

Como cada linha da tabela é computada de maneira similar, foi utilizado um _loop_ (laço de repetição). O _loop **while**_ funciona da seguinte forma:

- A condição entre parênteses é testada. Se for verdadeira (**fahr** é menor ou igual a **superior**), o corpo do _loop_, os _statements_ entre as chaves são executados;
- A condição é testada novamente, caso seja verdadeira, os _statements_ são executados novamente;
- Quando o teste for falso, isto é, a variável **fahr**(que é incrementada em 20 a cada _loop_) for maior do que a variável **superior**, o laço é encerrado e a execução do programa continua no _statement_ que o sucede.

No caso do programa-exemplo, não há _statement_ posterior ao **_while_**, então, o programa encerra. 

O corpo de um laço _**while**_ pode consistir de uma ou mais declarações fechadas por chaves ou uma única declaração sem a necessidade das chaves, isto é,

```c
  while (i > j)
    i = j + 2;
```

Nota-se que tanto no exemplo da temperatura quanto no anterior, os _statements_ dentro do laço são indentados (são inseridos espaços entre a margem e o início da linha, geralmente com um TAB do teclado). A indentação é importante para enfatizar a sequência lógica do programa, mostrando o que está dentro do _loop_. Além disso, é recomendado
utilizar espaços entre operadores e fazer apenas um _statement_ por linha para melhor leitura do código.

Voltando ao código da conversão Fahrenheit-Celsius, a maior parte do trabalho é feita dentro do _**while**_. A computação e atribuição (_assignment_) de valor à variável **celsius** é feita pela linha de código

```c
celsius = 5 * (fahr - 32) / 9;
```

A fórmula para conversão é 

![CodeCogsEqn](https://user-images.githubusercontent.com/69206952/136630550-b8dc6b88-83cd-42a6-ab0b-2426baa8fc61.png)

No entanto, ao invés de multiplicar **(fahr - 32)** por 5/9, a multiplicação por 5 foi feita antes, pois, em C, a divisão de inteiros é truncada, isto é, qualquer parte fracionária
é descartada, assim o resultado de 5/9 seria zero, resultando na variável **celsius** sempre nula. 

#### printf

Além disso, nesse exemplo também pode-se aprender mais sobre o funcionamento da função **printf**. O primeiro argumento dessa função sempre é a _string_ de caracteres a ser mostrada na saída, onde cada símbolo (**%**) indica que um dos outros argumentos (segundo, terceiro, ...) será substituído e em qual forma deverá ser impresso. Por exemplo, %d especifica um argumento do tipo inteiro.  

```c
 printf("%d\t%d\n", fahr, celsius);
```

Assim, a linha acima imprime na tela o valor dos dois inteiros **fahr** e **celsius** separados por um TAB (\t) e uma nova linha (\n) no final.

Cada termo com % é pareada com o segundo argumento, terceiro... Dessa forma, é necessário que o número (e tipo) de termos com %d na _string_ e o dos outros argumentos seja o mesmo para que não haja erros.

#### float

O programa de conversão de temperatura pode ser melhorado declarando as temperaturas como **float** ao invés de **int**. Assim, uma segunda versão do problema é mostrada abaixo:

```c
#include <stdio.h>
main(){
    float fahr, celsius;
    int inferior,superior,passo;
    inferior = 0;
    passo = 20;
    superior = 300;
    fahr = inferior;
    while (fahr <= superior){
        celsius = (5.0/9.0)*(fahr - 32.0);
        printf("%3.0f %6.1f\n", fahr, celsius);
        fahr = fahr + passo;
    }
}

```

que resulta em

![image](https://user-images.githubusercontent.com/69206952/136631737-641d6601-88e6-436a-9b94-5d4d1cead52e.png)

As diferenças entre este código e o anterior são poucas: a declaração de **fahr** e **celsius** como **_float_**. O uso de um ponto decimal em 5.0 e 9.0 indica que as constantes
são de ponto flutuante, permitindo a divisão sem truncamento. 

Deve-se notar que caso um operador matemático possua operandos inteiros, o resultado será inteiro. No entanto, se um dos operandos for **_float_** e o outro **int**, o resultado
é automaticamente convertido em **_float_**. Assim, caso fosse escrito **fahr - 32** ao invés de **fahr - 32.0**, o resultado seria convertido para ponto flutuante. Porém, para 
melhor leitura, é interessante indicar o ponto decimal. De mesmo modo, o teste **fahr <= superior** e a atribuição **fahr = inferior** ocorrem naturalmente (a variável do tipo **int** é convertida em **_float_** antes da operação.

A especificação **3.0f** no **printf** diz que um número de ponto flutuante (**fahr**) deve ser imprimido com largura de pelo menos 3 caracteres e nenhum ponto decimal e dígito fracionário. Já **%6.1f** indica que **celsius** é um número de ponto flutuante que deve ser impresso com largura mínima de 6 caracteres e 1 dígito após o ponto decimal. Na especificação do que deve ser impresso, a largura e o número de dígitos decimais podem ser omitidos. Assim, algumas opções são mostradas a seguir.

- %d : imprime um inteiro decimal;
- %6d : imprime um inteiro decimal com largura de pelo menos 6 caracteres;
- %f : imprime como ponto flutuante;
- %6f : imprime como ponto flutuante e largura de pelo menos 6 caracteres;
- %.2f : imprime como ponto flutuante e duas casas após o ponto decimal;
- %6.2f : imprime como ponto flutuante, largura de pelo menos 6 caracteres e duas casas após o ponto decimal.

Além disso, a função **printf** também reconhece:

- %o : octal;
- %x : hexadecimal;
- %c : caractere;
- %s : string de caracteres;
- %% : símbolo de %.

### The For Statement

Há diversas maneiras de escrever o mesmo programa. Uma variação do programa de conversão de temperatura é mostrada a seguir

```c
main() {
  int fahr;
  
  for (fahr = 0; fahr <= 300; fahr = fahr + 20)
    printf("%3d %6.1f\n", fahr, (5.0/9.0)*(fahr - 32));

}
```

Esse código produz o mesmo resultado. Uma das principais mudanças é a eliminação da maioria das variáveis.

O _statement **for**_ é um loop, uma generalização do _**while**_. Dentro dos parênteses do **_for_**, há três partes, separadas por ponto e vírgula.

1. A inicialização **fahr = 0**: é feita uma vez antes do programa entrar no _loop_.
2. O teste ou condição **fahr <= 300**: caso a condição seja verdadeira, o corpo do _loop_ é percorrido.
3. A expressão de iteração **fahr = fahr + 20**: após este incremento, a condição é reavaliada para o programa entrar ou não novamente no laço.

O _loop_ encerra caso a condição torne-se falsa. Da mesma forma do _while_, o corpo do laço de repetição pode ser uma linha única com um _statement_ ou vários _statements_ fechados por chaves.

### Symbolic Constants

Uma boa prática é definir certos números que são usados muitas vezes no código como uma constante, tornando o programa mais simples de ler e mais fácil de mudar quando necessário. Assim, um comando **#define** define um nome simbólico ou uma _symbolic constant_ como uma string de caracteres. Isto é, 

```c
#define    name    replacement text
```

Assim, qualquer ocorrência de **name** (não estando entre aspas ou parte de outro nome) será substituído por **replacement text**. O **name** tem a mesma forma do nome de uma variável, uma sequência de letras começando com uma letra. O **replacement text** pode ser composto por qualquer sequência de caracteres, não sendo limitado a números. Desse modo, no exemplo da temperatura, poderia-se criar as constantes a seguir:

```c
#define SUPERIOR 300
#define INFERIOR 0
#define PASSO 20
```

É costumeiro escrever o nome das constantes em letras maiúsculas para diferenciá-las de variáveis. Além disso, deve-se notar que não há ponto e vírgula no fim de uma linha **#define**.

### Character Input and Output

O modelo de entrada e saída suportado pela biblioteca padrão é muito simples. Entrada ou saída de texto, independente de sua origem ou de para onde vai, é lidada como _streams_ de caracteres. Uma _text stream_ é uma sequência de caracteres dividida em linhas; cada linha consiste de zero ou mais caracteres seguidas por um _newline character_ (\n).

A biblioteca padrão fornece diversas funções para leitura e escrita de um caractere por vez, das quais **getchar** e **putchar** são as mais simples. Cada vez que é chamada, a função **getchar** lê a próxima entrada de caractere de uma _text stream_ e a retorna. Assim, após

```c
c = getchar();
```

a variável **c** contém o próximo caractere da entrada (entradas são discutidas com mais ênfase no capítulo 7).

Já a função **putchar** imprime um **char** toda vez que é chamada. Logo,

```c
putchar(c);
```

imprime o conteúdo da variável inteira **c** como um caractere, usualmente na tela.

O código a seguir copia a entrada para a saída um caractere por vez.

```c

main() {

    int c;

    c = getchar();
    while (c != EOF) {
        putchar(c);
        c = getchar();
    }

}

```

O operador relacional != significa "não é igual a".

O que aparenta ser um caractere no teclado ou na tela é, como todas as outras coisas, armazenado internamente como um padrão de bits. O tipo **char** é especificamente feito para armazenar tais dados, mas o tipo **int** pode ser usado, e, neste caso, foi utilizado por uma razão importante.

O problema é distinguir o final da entrada de um dado válido. A solução é que **getchar** retorna um valor característico quando não há mais entrada, um valor que não pode ser confundido com qualquer caractere real. Tal valor é chamado **EOF** (end of file - fim do arquivo). Logo, deve-se declarar **c** como um tipo grande suficiente para armazenar qualquer valor que **getchar** retorne. Não se pode usar **char** já que **c** deve ser grande o suficiente para conter **EOF** em adição a qualquer **char** possível. Assim, usa-se **int**. (**EOF** é um inteiro definido em **<stdio.h>**).

Em C, qualquer _assignment_, como

```c
c = getchar();
```

é uma expressão e tem um valor, que é o valor do primeiro membro depois do _assignment_. Isso significa que tal atribuição pode aparecer como parte de uma expressão maior. Assim, se for colocado dentro da parte de teste do _loop_ _**while**_, o programa fica escrito como:

```c

#include <stdio.h>
main(){
  int c;
  
  while ((c = getchar()) != EOF )
    putchar(c);
}
```

Assim, o **_while_** pega um caractere, atribui a **c** e então testa se esse caractere é o sinal EOF. Se não for, o corpo do laço é executado, imprimindo o **char** e o while se repete. Quando o fim do arquivo é finalmente alcançado, o **_while_** termina, e, neste caso, **main** também.

Os parênteses ao redor do _assignment_ são necessários pois a precedência de != é maior do que a de =, o que significa que a ausência dos parênteses faria o teste (!=) antes do _assignment_ (=). Isto é, a atribuição

```c
c = getchar() != EOF
```

é equivalente a

```c
c = (getchar() != EOF)
```

O que causaria um efeito indesejado no código, atribuindo a **c** o valor de 0 ou 1.

#### Contagem de caracteres

O programa a seguir conta caracteres.

```c
#include <stdio.h>

main() {
    long nc;
    nc = 0;
    while (getchar() != EOF) {
        ++nc;
    }
    printf("%ld\n", nc); 
}
```

Há um pequeno problema na compilação do código, no qual o compilador nunca sai do laço, pois não recebe o sinal EOF. No compilador que eu utilizo, o EOF é o comando CTRL+Z, em alguns que vi na internet, CTRL+D.

O _statement_ **++nc;** apresenta um novo operador ++, que significa um incremento de 1. Seria o mesmo que escrever **nc = nc + 1**. Há um operador correspondente de decremento de 1 (**--**). Estes operadores podem ser sufixos ou prefixos e tem uma diferença sutil que será tratada no capítulo 2.

A especificação de conversão **%ld** diz ao **printf** que o argumento correspondente é um **_long integer_**.

Além do **long** (variável de pelo menos 32 bits), poderia-se lidar com números maiores ainda utilizando **double**. Mudando isso e trocando o _**while**_ por um _loop **for**_, tem-se:

```c
#include <stdio.h>

main() {
    double nc;
    for (nc = 0; getchar() != EOF; ++nc)
      ;
    printf("%.0f\n", nc);
}
```

Nota-se que o **printf** utiliza **%f** tanto para **_float_** quanto para **_double_**; Como já foi descrito, **%.0f** suprime o ponto decimal e a parte fracionária, que, neste caso, é zero.

O corpo desse _loop **for**_ é vazio, pois todo o trabalho de teste e incremento é feito dentro dos parâmetros da função. No entanto, as regras gramaticais do C exigem um corpo para o **_for_**. Dessa forma, o ponto e vírgula isolado - chamado _**null statement**_ - é escrito para satisfazer tal exigência.

Uma das principais vantagens dos _loops **while**_ e **_for_** é que o teste é feito antes de entrar no corpo do laço, dessa forma, os programas funcionam bem caso haja uma entrada nula.

#### Contagem de linhas

O programa a seguir conta linhas da entrada.

```c
#include <stdio.h>
main(){
  int c, nl;
  
  nl = 0;
  while ((c = getchar()) != EOF)
    if (c == '\n')
      ++nl;
  printf("%d\n", nl);
}
```

Agora, o corpo do **_while_** consiste de um **_if_** que controla o incremento da variável **nl** (número de linhas). O _statement **if**_ testa a condição entre parênteses, sendo verdadeira, o(s) _statement(s)_ são executados.

O duplo sinal de igualdade **==** é a notação em C para **é igual a**. Esse símbolo é utilizado para distinguir da igualdade simples **=** que é utilizada para atribuição de variáveis. 

Um caractere escrito entre aspas simples representa um valor inteiro igual ao valor numérico do caractere na máquina. Isso é chamado de _character constant_. Por exemplo, 'A' é uma constante de caractere; na tabela ASCII, seu valor é 65, a representação interna no caractere A. Da mesma forma, a sequência de escape '\n' representa o valor do caractere **_newline_**, que é 10 em ASCII.

#### Contador de palavras

Por fim, define-se uma palavra como uma sequência de caracteres que não contém um _blank_, um tab ou um _newline_. Assim, o programa a seguir é um contador de palavras, linhas e caracteres.

```c
#include <stdio.h>

#define DENTRO 1
#define FORA 0
main(){
    int c, nl, nw, nc, state;

    state = FORA;
    nl = nw = nc = 0;
    while ((c = getchar()) != EOF){
        ++nc;
        if (c == '\n')
            ++nl;
        if (c == ' ' || c == '\n' || c == '\t')
            state = FORA;
        else if (state == FORA){
            state = DENTRO;
            ++nw;
        }

    }
    printf("%d %d %d\n", nl, nw, nc);
}
```

Cada vez que o programa encontra a primeira palavra de uma letra, conta mais uma palavra. A variável **state** grava se o programa está, no momento, em uma palavra ou não. A preferência por DENTRO e FORA a 1 e 0 se dá pela melhor leitura do programa. Em códigos simples como esses, a diferença é mínima, no entanto, em programas maiores, é bastante útil para clarificar a leitura.

A linha 

```c
nl = nw = nc = 0;
```

atribui às três variáveis o valor 0. Isso não é um caso especial, mas uma consequência de que um _assignment_ é uma expressão com um valor e _assigments_ se associam da direita para a esquerda, portanto, a expressão acima equivale a esta:

```c
nl = (nw = (nc = 0));
```

O operador || significa OR (ou), logo, a linha de código

```c
  if (c == ' ' || c == '\n' || c == '\t')
```

pode ser lida como "se **c** é um _blank_ ou **c** é um _newline_ ou **c** é um tab". Há um operador correspondente && para o operador lógico AND (e), cuja precedência é maior do que a do OR. Expressões conectadas por && ou || são avaliadas da esquerda para a direita. É óbvio que neste caso se **c** for um _blank_, não é necessário testar as outras opções e o if realmente não as testa. No momento, não é algo particularmente importante, mas em situações mais complicadas, sim.

Este exemplo também mostra um **_else_** que especifica uma ação alternativa se a condição do **if** for falsa. A forma geral é

```c
if (expression)
  statement1
else 
  statement2
```

Somente um dos statements do _if-else_ é executado. Se **expression** é verdadeira, o _statement1_ é executado, se é falsa, o _statement2_ é executado.

Cada _statement_ pode ser uma expressão única ou várias entre chaves. No programa de contagem de palavras, o _statement_ depois do else é um **if** que controla outros dois _statements_ (o que é geralmente dito um **else if**).

### Arrays

Ao criar um programa para contar o número de ocorrências de cada dígito, de cada caractere de espaço em branco e de todos os outros, pode-se ilustrar vários aspectos de C em um programa.

Há doze categorias de entrada, então, é conveniente utilizar um _**array**_ para conter as ocorrências de cada dígito, ao invés de variáveis individuais. Abaixo, uma versão do programa:

```c
#include <stdio.h>

main() {
  int c, i, nwhite, nother;
  int ndigit[10];

  nwhite = nother = 0;
  for (i = 0; i < 10; ++i)
    ndigit[i] = 0;
  while ((c = getchar()) != EOF)
    if (c >= '0' && c <= '9')
      ++ndigit[c-'0'];
    else if (c == ' ' || c == '\n' || c == '\t')
      ++nwhite;
    else
      ++nother;

  printf("digits =");
  for (i = 0; i < 10; ++i)
    printf(" %d", ndigit[i]);
  printf(", white space = %d, other = %d\n",
    nwhite, nother);

}
```

![image](https://user-images.githubusercontent.com/69206952/136673121-9df104d5-4ccc-45d0-85dc-30f62441426f.png)

A linha de código 

```c
  int ndigit[10];
```

declara **ndigit** como um _array_ (vetor) de 10 inteiros. O subscrito de um _array_ sempre começa com 0 em C, então seus elementos são **ndigit[0], ndigit[1], ... ndigit[9]**. O subscrito pode ser qualquer expressão inteira, como a variável inteira **i** no exemplo. 

Este programa em particular utiliza propriedades da representação **char** dos dígitos. Por exemplo, o teste 

```c
  if (c >= '0' && c <= '9') ...
```

determina se o caractere em **c** é um dígito. Se sim, seu valor numérico é **c - '0'**. Isso funciona pois '0', '1', ..., '9' tem valores consecutivos crescentes. Além disso, na tabela ASCII, o valor de '0' é 48. Dessa forma, **c - '0' = c - 48**, assim, quando c, for '1' (ASCII - 49), por exemplo, **c - 48 = 1**.

### Funções

Uma função fornece um modo conveniente de encapsular alguma computação que pode ser usada posteriormente sem preocupar-se com sua implementação. Até o momento só foram usadas funções disponibilizadas por bibliotecas, agora é o momento de escrever algumas. 

A linguagem C não possui o operador de exponenciação, então vamos escrever uma função **power (m,n)** para elevar um inteiro **m** a um inteiro positivo **n**. Isto é, o valor de **power (3,2)** seria 9, por exemplo. (A biblioteca padrão contém a função **pow(x,y)** que computa x<sup>y</sup>).

Assim, o seguinte código possui a função **power** e um programa **main** para executá-la.

```c
#include <stdio.h>

int power(int m, int n);

main(){
  int i;
  
  for (i = 0; i < 10; ++i)
    printf("%d %d %d\n", i, power(2,i), power(-3,i));
  return 0;
  
}

int power(int base, int n){
  int i, p;
  
  p = 1;
  for (i = 1; i <= n; ++i)
    p = p * base;
  return p;
}
```

A definição de uma função tem a forma de:

```
tipo-de-retorno nome-da-função(declaração de parâmetros, caso haja){
  declaracões
  statements
}
```

A definição de funções pode aparecer em qualquer ordem e ainda, num arquivo fonte único ou em vários, no entanto, nenhuma função pode ser dividida em vários arquivos. 

A função **power** é chamada duas vezes pela **main** na linha

```c
  printf("%d %d %d\n", i, power(2,i), power(-3,i));
```

Cada chamada passa dois argumentos para **power**, que retorna um inteiro para ser formatado e imprimido.

A primeira linha da função **power**

```c
  int power(int base, int n)
```

declara os nomes e tipos dos parâmetros e o tipo de resultado que a função retorna. Os nomes utilizados por **power** para seus parâmetros são locais a **power** e não são visíveis a outras funções, isto é, outras funções podem utilizar os mesmos nomes sem conflito algum. Pode-se observar, por exemplo que a variável **i** declarada dentro de **power** é completamente não relacionada a **i** declarada em **main**.

O livro geralmente trata da seguinte forma:

- Parâmetro: variável nomeada numa lista entre parênteses na definição de uma função;
- Argumento: o valor usado na chamada da função.

O valor que **power** computa é retornado a **main** pelo _statement_ **return**. Qualquer expressão pode seguir **return**. Não é necessário que uma função retorne um valor.

No exemplo anterior, **main** retorna um valor. Já que **main** é uma função como qualquer outra, ela pode retornar um valor para quem a chama (neste caso, o ambiente que a executa). Tipicamente um retorno de valor nulo implica terminação normal. Valores diferentes de zero sinalizam terminação errônea ou incomum. Até o momento, os **return** de **main** estavam sendo omitidos, mas serão incluídos a partir de agora, como lembrete de que programas devem retornar status ao seu ambiente.

A declaração

```c
  int power(int m, int n);
```

antes de **main** indica que **power** é uma função que espera dois argumentos **int** e retorna um **int**. Essa declaração, chamada de _function prototype_, deve concordar com a definição e utilização de **power**. No entanto, o nome dos parâmetros não precisa ser o mesmo. Na verdade, o nome dos parâmetros é opcional num _function prototype_, então poderia ser escrito como

```c
  int power(int, int);
```

### Arguments - Call by Value

Em C, os argumentos de funções são passados "por valor", isto é, a função recebe o valor em variáveis temporárias, não nas originais. Assim, a função chamada não pode alterar diretamente uma variável na função que a chamou, somente a cópia privada, temporária.

O código a seguir é uma versão de **power** que utiliza essa propriedade.

```c
  int power(int base, int n){
    int p;
    
    for (p = 1; n > 0; --n)
      p = p * base;
    return p;
  
  }
```

O parâmetro **n** é usado como uma variável temporária, eliminando a variável **i**. O que quer que seja feito com a variável **n** dentro de **power** não tem efeito no argumento com o qual **power** foi originalmente chamada. 

Com vetores, é diferente. Quando o nome de um _array_ é utilizado como argumento, o valor passado à função é a localização (ou endereço) do começo do vetor - não há cópia dos elementos do vetor. Assim, a função tem acesso e pode alterar qualquer elemento do _array_, como é discutido na próxima seção.

### Character Arrays

O tipo mais comum de _array_ em C é o de caracteres. Para ilustrar o uso de _character arrays_ e função que os manipulam, escrevemos um programa que lê um conjunto de linhas de texto e imprime a mais longa. Assim, o algoritmo seria

```
  while (existe outra linha)
    if (é maior do que a linha anterior)
      salva a linha
      salva o seu tamanho
  imprime a maior linha
```

O programa se divide em partes:

1. Receber uma nova linha;
2. Testar a linha recebida;
3. Salvar uma linha;
4. Controlar o processo.

Assim, vamos escrever uma função separada **getline** para buscar a próxima linha de entrada. Quando uma das linhas encontradas for maior que a maior anterior, deve ser salva em algum lugar, sugerindo uma segunda função **copy** para copiá-la para um local seguro. E deve-se ter um programa principal (main) para controlar as funções. Assim,

```c
#include <stdio.h>
#define MAXLINE 1000

int getline(char line[], int maxline);
void copy(char to[], char from[]);

main(){

    int len; // tamanho da linha atual
    int max; // tamanho máximo até o momento
    char line[MAXLINE]; // linha atual
    char longest[MAXLINE]; // linha maior atualmente

    max = 0;
    while ((len = getline(line, MAXLINE)) > 0 )
        if (len > max){
            max = len;
            copy(longest, line);
        }
    if (max > 0)
        printf("%s", longest);
    return 0;
}

int getline(char s[], int lim)
{
    int c, i;

    for (i = 0; i < lim - 1 && (c = getchar()) != EOF && c != '\n'; ++i)
        s[i] = c;
    if (c == '\n'){
        s[i] = c;
        ++i;
    }
    s[i] = '\0';
    return i;

}

void copy(char to[], char from[])
{
    int i;

    i = 0;
    while ((to[i] = from[i]) != '\0')
        ++i;
}

```

As funções **getline** e **copy** são declaradas no início do programa. **main** e **getline** se comunicam por meio de um par de argumentos e um valor retornado. Em **getline**, os argumentos são declarados na linha

```c
  int getline(char s[], int lim)
```

a qual especifica que o argumento **s** é um vetor e **lim** é um inteiro. O comprimento do vetor **s** não é necessário em **getline**, pois seu tamanho é estabelecido em **main**. Essa linha também mostra que **getline** retorna um **int**; como **int** é o tipo padrão de retorno, pode ser omitido.

Algumas funções são usadas apenas pelo seu efeito e não retornam nenhum valor. O tipo de retorno de **copy** é **void**, significando que esta não retorna nenhum valor. 

**getline** coloca o caractere '\0' (_**null character**_) no final do _array_ que está criando para marcar o final da _string_ de caracteres. Essa convenção é utilizada em C, isto é, quando uma _string_ constante como **"hello\n"** aparece em um programa escrito em C, é armazenada como um vetor de caracteres contendo os caracteres da string terminados por um '\0' para marcar o final, como mostra a figura abaixo.

![image](https://user-images.githubusercontent.com/69206952/136675756-a21782cf-f670-48e0-ab4a-dcf06e86ea1e.png)

O formato **%s** em **printf** espera como argumento correspondente uma _string_ representada dessa forma. **copy** também utiliza este fato e copia este caractere para o argumento de saída. 

Analisando os limites, é impossível ao usuário de **getline** saber antecipadamente quão grande uma entrada pode ser, assim **getline** faz uma checagem de **_overflow_** (transbordamento).

### External Variables and Scope

As variáveis criadas em **main**, como **line** e **longest** no exemplo anterior, são locais a **main**. Por serem declaradas dentro de **main**, nenhuma outra função pode ter acesso direto a elas. O mesmo é válido pra outras variáveis em outras funções. Cada variável local passa a existir somente quando a função é chamada e desaparece quando a função é encerrada. Essas variáveis são conhecidas como _automatic variables_. (No capítulo 4, é discutido a classe **static** na qual variáveis locais retém seus valores entre chamadas).

Como uma alternativa, é possível definir variáveis que são **externas** a todas as funções, i.e., variáveis que podem ser acessadas por nome por qualquer função. Uma variável externa deve ser definida, exatamente uma vez, fora de qualquer função, alocando armazenamento para si.

Antes de uma função poder utilizar uma variável externa, o nome da variável deve ser "apresentado" à função. Uma forma de fazer isso é escrever **extern** antes da declaração. Em algumas circunstâncias, esse termo pode ser omitido, caso a definição da variável externa ocorra no arquivo fonte antes do seu uso em uma função particular. Portanto, é prática comum colocar as definições de todas as variáveis externas no começo do arquivo fonte, omitindo todas as declarações **extern**.

Caso o programa seja escrito em diversos arquivos e uma variável é definida no _arquivo1_ e utilizada em _arquivo2_ e _arquivo3_, deve haver declarações **extern** em _arquivo2_ e _arquivo3_. A prática mais usual é´coletar as declarações **extern** de variáveis e funções em um arquivo separado, historicamente chamado de _**header**_, que é incluido pela diretiva **#include** na frente de cada arquivo fonte. O sufixo **.h** é convencional para nomes de _header_. As funções da biblioteca padrão, por exemplo, são declaradas em _headers_ como **<stdio.h>**. (Esse tópico é discutido com mais profundidade no capítulo 4).

- Uma prática interessante para compatibilidade com versões antigas de programas C é utilizar a palavra **void** quando uma lista de argumentos for vazia, isto é,

```c
int main(void) ...
```

Vale ressaltar que:

- **Definição** de uma variável se refere ao momento em que a variável é criada ou é atribuido um armazenamento para tal;
- **Declaração** de uma variável se refere ao momento no qual a natureza da variável é declarada, mas nenhum armazenamento é alocado.

Por fim, é importante notar que depender apenas de variáveis externas pode parecer tentador, mas pode ocasionar problemas, pois as variáveis estarão lá mesmo quando não necessárias. A conexão de dados entre funções não é muito clara, pois variáveis podem ser modificadas em maneiras inesperadas e o programa torna-se difícil de mudar.

O capítulo 1 do livro cobre o que pode ser chamado de núcleo convencional da linguagem C. É possível escrever programas úteis de tamanho considerável com os blocos construtores aprendidos aqui.

  </div>
