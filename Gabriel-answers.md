# Exercise 1
* `w01-byte` bytes/second: <!-- Fill this in -->
* `w02-byte` bytes/second: <!-- Fill this in -->
* `w03-byte` bytes/second: <!-- Fill this in -->

# Exercise 2
### Scenario 1:
* How many array elements can fit into a cache block?
<!-- 2  -->
* What combination of parameters is producing the hit rate you observe? Think about the sizes of each of the parameters.
<!-- O tamanho do bloco, que cada bloco pode ter 2 elementos do array, o stepsize, que possibilita a utilização do mesmo bloco, e a opção, porque faz um tipo de acesso diferente -->

* What is our hit rate if we increase Rep Count arbitrarily? Why?
<!-- 50% todas as vezes, porque cada bloco carrega 2 elementos do array, então quando ele erra o primeiro número, ele acerta o segundo, então cada 2 acessos acerta uma vez -->

### Scenario 2:
* What combination of parameters is producing the hit rate you observe? Think about the sizes of each of the parameters.
<!--Como há 128 bytes no array, ou 32 elementos e o stepsize é 27, ele nunca acertará, já que carregará 2 elementos, moverá 27 e então carregará 2 elementos diferentes, ele também acessa 4 vezes porque o repcount é 2 -->

* What happens to our hit rate if we increase the number of blocks and why?
<!-- ele terá 50% de taxa de acerto, carregará ambos os endereços, e na segunda vez que for executado, acertará ambos os endereços -->

### Scenario 3:
* Choose a `number of blocks` greater than `1` and determine the smallest `block size` that uses every block *and* maximizes the hit rate given the parameters above. Explain why.
Number of blocks: <!-- 32, então o cache pode armazenar todo o array, na primeira vez que for executado, ele tem uma taxa de acerto de 50%, mas na segunda execução ele tem tudo dentro do cache, então ele apenas acerta.-->

Block Size: <!--  8, para cada passo ele carrega 2 elementos para o array-->

# Exercise 3
* Order the functions from fastest to slowest, and explain why each function's ranking makes sense using your understanding of how the cache works. Some functions might have similar runtimes. If this is the case, explain why.
<!-- O mais rápido é kji, então temos jki, ijk, jik, kij e o mais lento é ikj. Primeiro, vamos considerar que os blocos de cache podem conter uma linha inteira de cada array e, claro, cada acesso carrega uma linha inteira do array no cache. Na ordem kji, o array A é lido por linha, então ele carrega uma linha e usa todos os elementos antes de carregar mais uma linha, o array B é o oposto, ele carrega uma linha, mas é acessado na ordem collum, então ele lê uma linha, mas usa apenas um elemento n vezes, e então ele carrega mais uma linha, e o array C é similar a A, ele carrega uma linha, usa tudo, e depois carrega outro. Tudo isso significa que C e A têm ótima localidade, B não tanto, mas isso se transforma no melhor cenário. A ordem mais lenta ikj é o oposto, o array C muda de linha a cada iteração, o array A carrega uma linha e usa o mesmo elemento n vezes e carrega outra linha, e o array B carrega uma linha a cada iteração, significando que B e C são usados muito mal e A também é muito ruim, já que ele carrega n elementos mas usa apenas 1.->
