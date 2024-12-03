# Exercise 1
* `w01-byte` bytes/second: 
**RESPOSTA: 225280 bytes   404.811 sec   556.507 byte/sec (pensava que era mais rápido fazer uma chamada para o sistema)**
* `w02-byte` bytes/second: 
**RESPOSTA: 5120000 bytes   10.289 sec   497604 byte/sec**
* `w03-byte` bytes/second: 
**RESPOSTA: 5120000 bytes   0.213 sec   2.40056e+07 byte/sec (bem rápido LOL)**

# Exercise 2
### Scenario 1:
* How many array elements can fit into a cache block?
**RESPOSTA: 2 inteiros ou 2 words.**

What combination of parameters is producing the hit rate you observe? Think about the sizes of each of the parameters.

**RESPOSTA: Rep Count está fazendo acessar cada elemento do vetor 2 vezes, por isso temos 64 acessos.
Step Size está percorrendo o vetor elemento a elemento, que aliado ao
tamanho do bloco (BLOCK SIZE) o qual contém 2 elementos do vetor por bloco,
causa 1 miss (ao ler a primeira vez) e 1 hit (pois o elemento adjacente
já está no bloco).
Option também influencia, uma vez que a opção 0 acessa 1 vez somente o vetor (escrita), e a opção 1 acessa 2 vezes o vetor (leitura e escrita).
O tamanho do vetor (Array Size), já que aumentando o tamanho acontecerão mais misses.**

* What is our hit rate if we increase Rep Count arbitrarily? Why?

**RESPOSTA: Será sempre 0.5, pois ao acessar um bloco acontecerá primeiro um miss e depois um hit (visto que o tamanho do bloco são duas words)**

### Scenario 2:
* What combination of parameters is producing the hit rate you observe? Think about the sizes of each of the parameters.

**RESPOSTA: Os mesmos do cenário 1, no entanto o que influencia mais é: STEP SIZE, uma vez que o primeiro acesso do vetor é na posição 0 e depois 27 elementos depois prejudicando a localidade espacial.**

* What happens to our hit rate if we increase the number of blocks and why?

**RESPOSTA: Aumenta para 0.5, pois, na primeira iteração, com dois blocos ou mais na cache, primeiro acontecerá um miss, e trazendo o primeiro bloco para a posição 0 da cache e 27 elementos depois acontece outro miss trazendo o segundo bloco para a cache. O loop reinicia e os valores que serão escritos já estão na cache**

### Scenario 3:
* Choose a `number of blocks` greater than `1` and determine the smallest `block size` that uses every block *and* maximizes the hit rate given the parameters above. Explain why.
Number of blocks: **2 blocos** 
Block Size: **256 bytes**

**RESPOSTA: Ao ter um bloco de tamanho 256 (tamanho do array) o primeiro acesso será um miss e os demais acessos serão hit (terá carregado o array inteiro no bloco após o miss), aproveitando a localidade espacial.**

# Exercise 3
* Order the functions from fastest to slowest, and explain why each function's ranking makes sense using your understanding of how the cache works. Some functions might have similar runtimes. If this is the case, explain why.

**RESPOSTA:
da mais rápida para a mais lenta: <br>
    multMat4 (jki): 0,471 Gflop/s <br>
    multMat6 (kji): 0,467 Gflop/s <br>
    multMat1 (ijk): 0,381 Gflop/s <br>
    multMat3 (jik): 0,277 Gflop/s <br>
    multMat5 (kij): 0,186 Gflop/s <br>
    multMat2 (ikj): 0,173 Gflop/s <br>**

  **As mais rápidas são as de ordem jki e kji, ambas são semelhantes, a primeira ordem (jki) aproveita localidade espacial das matrizes C e A, iterando sequencialmente pela linha da matriz. Aproveita-se a localidade temporal e espacial da matriz B, pois seus elementos são acessados sequencialmente na cache e como somente no loop intermediário ela avança para o próximo elemento a localidade temporal é bem aproveitada.
  Para a ordem kji, a qual é tão rápida quanto jki, a ideia é a mesma, os elementos de C e A são acessados sequencialmente e aproveita-se da localidade temporal dos elementos de B a qual é acessada por colunas. 
  Para as multiplicações mais lentas (ikj e kij) o que acontece é: não há acesso sequencial dos elementos das matrizes, causando perda de performance. A localidade temporal também é afetada uma vez que as linhas das matrizes podem ocupar o mesmo indíce na memória cache (suposição uma vez que nos computadores atuais a cache é conjunto-associativa).**
