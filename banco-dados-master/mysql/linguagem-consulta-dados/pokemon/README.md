# Pokémon

Há mais de 10 anos, crianças do mundo inteiro vêm descobrindo o mundo encantado dos Pokémon. Hoje, a família de produtos Pokémon inclui videogames, o jogo Pokémon Estampas Ilustradas, a série de TV animada, filmes, brinquedos e muito mais. Muitos pais acreditam que o Pokémon Estampas Ilustradas e os videogames do Pokémon estimulam seus filhos a aprender a ler, já que a leitura é indispensável na maioria dos jogos do Pokémon. Os jogos também estimulam o pensamento estratégico e, em muitos casos, habilidades matemáticas básicas. O Pokémon valoriza muito o espírito esportivo e o respeito pelos outros jogadores.

## O que são Pokémon?

Pokémon são criaturas de todas as formas e tamanhos que convivem com os humanos na natureza. Na grande maioria, os Pokémon não falam, exceto para proferir seus nomes. Os Pokémon são criados e comandados por seus donos (os chamados "Treinadores"). No decorrer das aventuras, os Pokémon crescem e ganham experiência, podendo até mesmo evoluir para Pokémon mais fortes. Alguns Pokémon, como Pikachu, Piplup e Charizard, possuem papéis de destaque na série de videogames, no jogo Estampas Ilustradas e nos programas de TV, mas eles são apenas algumas das quase 500 criaturas que habitam o universo dos Pokémon.

**Fonte:** [Webiste Oficial - Pokémon](https://www.pokemon.com/br/guia-para-pais/)


## Ponto de Partida

Para começar esse exercício, você deverá: 

* 1. Pegar o arquivo `pokedex_create_v1.sql`, disponível na pasta [data](data/)
* 2. Abrir o software [MySQL](https://www.mysql.com/products/workbench/)
* 3. Exectuar o script para importar um novo banco de dados 


## Resumo do Projeto

Para este projeto, sua tarefa é criar consultas (queries), usando as técnicas da [Linguagem de Consulta de Dados](https://github.com/profdiegoaugusto/banco-dados/tree/master/mysql/linguagem-consulta-dados) no banco de dados `pokedex` do universo Pokémon. O esquema do banco de dados possui apenas uma tabela chamada `Pokémon`, com as seguintes colunas:

| Coluna          | Descrição                                                                                                                                                                                                                        |
|-----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| numero          | Chave Primária: o número do Pokémon no Pokedex Nacional                                                                                                                                                                          |
| nome            | Nome do Pokémon                                                                                                                                                                                                                  |
| tipo1           | Todas as criaturas Pokémon e seus movimentos recebem determinados tipos. Cada tipo tem vários pontos fortes e fracos no ataque e na defesa, ou seja, cada Pokémon tem um tipo que determina sua fraqueza/resistência aos ataques |
| tipo2           | O tipo secundário do Pokémon caso ele possua                                                                                                                                                                                     |
| total           | Soma de todas as estatísticas básicas (Pontos de Vida, Ataque, Defesa, Ataque Especial, Defesa Especial e Velocidade)                                                                                                            |
| hp              | HP (Hit Points ou Health Points), define quanto dano um Pokémon pode suportar antes de desmaiar                                                                                                                                  |
| ataque          | O ataque base do Pokémon                                                                                                                                                                                                         |
| defesa          | A defesa base do Pokémon                                                                                                                                                                                                         |
| ataque_especial | O ataque especial base do Pokémon                                                                                                                                                                                                |
| defesa_especial | A defesa especial base do Pokémon                                                                                                                                                                                                |
| velocidade      | A velocidade base do Pokémon                                                                                                                                                                                                     |
| geracao         | Número da geração em que o Pokémon foi introduzido                                                                                                                                                                               |
| lendario        | Valor Booleano que indica se o Pokémon é lendário ou não                                                                                                                                                                         |
| cor             | A cor do Pokémon                                                                                                                                                                                                                 |
| altura_m        | Altura em metros do Pokémon                                                                                                                                                                                                      |
| peso_kg         | Peso em Kilos do Pokémon                                                                                                                                                                                                         |
| taxa_captura | A taxa de captura do Pokémon é um número entre 0 e 255, quanto maior, melhor |


## Consultas

1. Selecione o banco de dados (esquema) `pokédex`.

```sql
USE pokedex;
```

2. Obtenha informações da estrutura da tabela `Pokémon`.

```sql
DESCRIBE pokemon; 
```

3. Selecione todos os pokémons cadastrados no banco de dados.

```sql
SELECT * FROM POKEMON ;
```

4. Selecione o `numero`, `nome`, `cor`, `altura_m` e `peso_kg` de todos os pokémons cadastrados.

```sql
SELECT numero, nome, cor, altura_m, peso_kg FROM Pokemon;
```

5. Qual é o `numero` e o `nome` de todos os pokémons da primeira geração?

```sql
SELECT numero, nome FROM pokemon where geracao = 1;
```

6. Quais são os pokémons `Amarelo` da primeira geração?

```sql
SELECT * FROM pokemon where cor= 'amarelo'AND geracao = 1;
```

7. Qual é o pokémon mais forte?

```sql
SELECT * FROM pokemon ORDER BY total DESC LIMIT 1; 
```


8. Selecione o `numero`, `nome` e `tipo1`; de todos os pokémons cujo tipo primário é `Fire`.

```sql
SELECT numero, nome, tipo1 FROM pokemon WHERE tipo1 = 'fire'; 
```

10. Selecione em ordem decrescente o `numero`, `nome` e `defesa` de todos os pokémons.

```sql
SELECT numero, nome, defesa FROM pokemon ORDER BY numero, nome, defesa DESC ; 
```


11. Qual o pokémon possui *menor* taxa de captura? Selecione apenas `numero` e `nome`.

```sql
SELECT numero, nome FROM pokemon ORDER BY taxa_captura ASC LIMIT 1;
```


12. Selecione todos pokémons que não possuem tipo secundário, ou seja, `tipo2`.

```sql
SELECT * FROM pokemon WHERE tipo2 IS NULL; 

```

13. Selecione `numero`, `nome`, `tipo1`, `tipo2` de todos os pokémons que possuem o peso entre 100kg e 500kg.

```sql
SELECT numero, nome, tipo1, tipo2 FROM pokemon ORDER BY peso_kg BETWEEN 101 AND 499;
```


14. Crie um ranking dos top 10 pokémons mais velozes, contendo `numero`, `nome` e `velocidade`.

```sql
SELECT numero, nome, velocidade FROM pokemon ORDER BY velocidade DESC LIMIT 10;
``` 


15. Selecione `numero`, `nome`, `tipo1`, `tipo2`, `taxa_captura` dos pokémons que possuem os dois tipos e tenham uma taxa de captura acima de 100. Ordene os resultados decrescente pela taxa de captura.

```sql
SELECT numero, nome, tipo1, tipo2, taxa_captura FROM pokemon WHERE tipo1 IS NOT NULL AND taxa_captura > '100' AND tipo2 IS NOT NULL ORDER BY taxa_captura DESC;
```

16. Quais são os tipos primários dos pokémons?

```sql
SELECT DISTINCT tipo1 FROM pokemon; 
```

17. Selecione o `numero`, `nome` e `cor`; de todos os pokémons que o nome começa com a letra `D`.

```sql
SELECT nome, numero, cor FROM pokemon WHERE nome LIKE 'D%';
```

18. Qual é o pokémon mais poderoso de todas as gerações?

```sql
SELECT nome FROM pokemon ORDER BY total DESC LIMIT 1;
```

19. Selecione o `numero`, `nome`, `defesa`, `ataque` dos pokémons com defesa > 60 e ataque <= 70; ordenados decrescente pelo `total`. 

```sql
SELECT nome, numero, defesa, ataque FROM pokemon WHERE defesa > 60 AND ataque <=70 ORDER BY total DESC;
```

20. Selecione todos os pokémons do tipo `Planta` e `Venenoso` que não sejam `Green`, ordenado crescente pelo `nome`.

```sql
SELECT * FROM pokemon WHERE tipo1 = 'planta' AND tipo2 = 'venenoso' AND NOT cor = 'Green' ORDER BY nome ASC;
```

21. Selecione de maneira crescente os nomes dos pokémons que possuem a letra y na 4ª posição do nome.

```sql
SELECT nome FROM pokemon WHERE nome LIKE '___y%' ORDER BY nome ASC;
```

22. Qual é o maior valor de `ataque_especial` cadastrado?

```sql
SELECT nome, ataque_especial FROM pokemon WHERE ataque_especial ORDER BY ataque_especial DESC LIMIT 1;
```

23. Selecione o `numero`, `nome` e `altura_m` dos pokémons que possuem altura acima de 2,10m.

```sql
SELECT nome, numero, altura_m FROM pokemon WHERE altura_m > '2,10';
```

24. Quais são as diferentes tipos de cores dos pokémons? Apresente os resultados de maneira crescente pelo nome da cor.

```sql
SELECT nome, cor FROM pokemon ORDER BY cor ASC;
```

25. Selecione o `nome` e `velocidade` dos pokémons com velocidade entre 30 e 70. Ordene os resultados por nome (crescente) e velocidade (decrescente)

```sql
SELECT nome, velocidade FROM pokemon WHERE velocidade BETWEEN 29 AND 69 ORDER BY nome ASC, velocidade DESC;
```

26. Quem são os pokémons lendários? Apresente os resultados ordenados por `total` decrescente.

```sql
SELECT nome FROM pokemon WHERE lendario ORDER BY total DESC;
```


27. Selecione os pokémons da primeira geração com taxa de captura igual a 255.

```sql
SELECT nome, taxa_captura, geracao FROM pokemon WHERE geracao = '1' AND taxa_captura = '255';
```


28. Quem é o mais poderoso? selecione o `Pikachu`, `Squirtle`, `Bulbasaur` e `Charmander`; ordenados decrescente pelo `total`. 

```sql
SELECT nome FROM pokemon WHERE nome IN ('pikachu', 'Squirtle', 'Bulbasaur', 'Charmander') ORDER BY total DESC; 
```

29. Quem são os pokémons da primeira geração, que começam com a letra `d` e não possuem tipo secundário?
Ordene os resultados crescente por `taxa_captura` e decrescente pelo `total`.

```sql
SELECT nome FROM pokemon WHERE geracao = '1' AND nome LIKE 'D%' AND NOT tipo2 ORDER BY taxa_captura ASC, total DESC;
```

30. Qual é o ranking dos top 5 pokémons lendários com maior `taxa_captura` e `total`? Apresente apenas `numero, nome, total, taxa_captura` nos resultados.

```sql
SELECT nome, numero, taxa_captura, total FROM pokemon WHERE lendario = '1'  ORDER BY taxa_captura, total DESC LIMIT 5;
```

31. Selecione o `numero`, `nome`, `peso_kg` dos pokémons com peso entre 2kg e 3kgs?

```sql
SELECT nome, numero, peso_kg FROM pokemon WHERE peso_kg BETWEEN '1.99' AND '2.99';
```

32. Selecione o `numero`, `nome`, `tipo1` e `tipo2` dos pokémons com tipo primário `Normal`, que não possuem tipo secundário. Existe algum pokémon lendário nos resultados, se sim, os remova dos resultados?

```sql
  SELECT nome, numero, tipo1, tipo2 FROM pokemon WHERE tipo1 = 'normal' AND tipo2 IS NULL AND lendario = '0';
```

33. Quem são os pokémons do tipo `Water` que não são azuis? Apresente `numero`, `nome`, `tipo1`, `tipo2` e `cor`, ordenados pelo `nome` de maneira crescente.

```sql
 SELECT nome, numero, tipo1, tipo2, cor FROM pokemon WHERE NOT cor = 'Blue' AND tipo1 = 'Water' OR tipo2 = 'Water' ORDER BY nome ASC;
```

34. Crie um ranking dos top 10 pokémons mais lentos.

```sql
SELECT numero, nome, velocidade FROM pokemon WHERE velocidade ORDER BY velocidade ASC LIMIT 10;
```

35. Selecione os pokémons cujo nome comece e termine com a letra `a`. 

```sql
SELECT nome FROM pokemon WHERE nome LIKE 'A%a';
```

36. Quem são os pokémons do tipo `Fire` que não são vermelhos? Apresente `numero`, `nome`, `tipo1`, `tipo2` e `cor`, ordenados pelo `nome` de maneira crescente.

```sql
 SELECT nome, numero, tipo1, tipo2, cor FROM pokemon WHERE NOT cor = 'Red' AND tipo1 = 'Fire' OR tipo2 = 'Fire' ORDER BY nome ASC;

```

37. Quais são os diferentes tipos de `peso_kg` dos pokémons? Apresente os resultados ordenados de maneira crescente.

```sql
SELECT DISTINCT peso_kg FROM pokemon ORDER BY peso_kg ASC;
```

38. Selecione o `numero`, `nome` e `hp` dos pokémons com valores entre 0 e 100. Ordene os resultados de maneira crescente por `hp` e `nome`.

```sql
SELECT DISTINCT numero, nome, hp FROM pokemon WHERE hp BETWEEN '0' AND '99' ORDER BY hp, nome ASC;
```

39. Selecione o `numero`, `nome`, `hp`, `ataque`, `defesa` e `total`; dos pokémons com valores de `hp`, `ataque`, `defesa` maiores ou iguais a 100.

```sql
SELECT DISTINCT numero, nome, hp, ataque, defesa, total FROM pokemon WHERE hp >= '100' AND ataque >= '100' AND defesa >= '100';
```

40. Selecione todos os pokémons do tipos `Water` e `Gelo`, ordenados decrescente por `total`.

```sql
SELECT DISTINCT numero, nome, tipo1, tipo2, total FROM pokemon WHERE tipo1 = 'Water' OR tipo2 = 'Water' AND tipo1 = 'Gelo' OR tipo2 = 'Gelo' ORDER BY total DESC;
```


## REFERÊNCIAS

* [Webiste Oficial - Pokémon](https://www.pokemon.com/br/guia-para-pais/)
* [Guia de Estilo SQL · SQL Style Guide](https://www.sqlstyle.guide/pt-br/)







