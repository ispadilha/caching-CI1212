# Exercise 1
* `w01-byte` bytes/second: <!-- 1189.72 -->
* `w02-byte` bytes/second: <!-- 483452 -->
* `w03-byte` bytes/second: <!-- 3.93295e+07 -->

# Exercise 2
### Scenario 1:
* How many array elements can fit into a cache block?
<!-- Assumindo sizeof(int) = 4 e tendo definido block size = 8, são portanto 2 elementos por bloco. -->
* What combination of parameters is producing the hit rate you observe? Think about the sizes of each of the parameters.
<!-- O tamanho do bloco de cache, relativamente pequeno (8B) em relação ao tamanho do array (128B). -->
* What is our hit rate if we increase Rep Count arbitrarily? Why?
<!-- Continuará perto de 0.5, pois cada bloco de cache comporta 2 elementos apenas; e com um step-size igual a 1, os mesmos são constantemente carregados e substituídos. -->

### Scenario 2:
* What combination of parameters is producing the hit rate you observe? Think about the sizes of each of the parameters.
<!-- O array com 128B (ou 32 elementos) e o step-size desproporcional de 27, o qual faz com que grandes porções de memória sejam "puladas" ao carregar os blocos.
Isso faz com que quaisquer dois acessos contíguos não usem o mesmo bloco de cache, mantendo assim o hit-rate em zero. -->
* What happens to our hit rate if we increase the number of blocks and why?
<!-- Mais blocos do array poderão ser armazenados em cache, potencialmente o array inteiro. Neste caso, mesmo com o step-size grande demais, aumentam as chances de "hit" e diminuem as de precisar substituir blocos. -->

### Scenario 3:
* Choose a `number of blocks` greater than `1` and determine the smallest `block size` that uses every block *and* maximizes the hit rate given the parameters above. Explain why.
Number of blocks: <!-- 32, pois possibilita guardar todo o array em cache, evitando precisar substituir blocos. -->
Block Size: <!-- 8, pois com o array tendo 256 bytes, dividindo isso pelo número de blocos acima, chegamos ao tamanho de cada bloco sendo igual a 8. Além disso, é mantido alinhamento com o padrão de acessos (step-size igual a 2). -->

# Exercise 3
* Order the functions from fastest to slowest, and explain why each function's ranking makes sense using your understanding of how the cache works. Some functions might have similar runtimes. If this is the case, explain why.
<!-- Os tempos encontrados, para as diferentes ordens de iterações/loops, da mais lenta para a mais rápida, foram:
    ikj (0.165 Gflop/s), kij (0.166 Gflop/s), jik (0.309 Gflop/s), ijk (0.321 Gflop/s), kji (0.425 Gflop/s), jki (0.426 Gflop/s).
    Os casos mais lentos (ikj e kij), colocam o índice "j" sendo tratado como o loop mais interno. Assim, apresentam baixa localidade espacial nas matrizes B e C, e também baixa localidade temporal, pois carregamentos para cache não são bem reutilizados.
    Os casos intermediários (ijk e jik) deixam os loops dos índices "i" e "j" como externos, o que melhora a localidade espacial na matriz C.
    Os casos mais rápidos colocam o loop de índice "i" como internos, o que melhora muito a localidade espacial, pois as matrizes "internas" são carregadas a cada linha.
-->
