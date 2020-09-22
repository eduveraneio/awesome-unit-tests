# testes-unidade
Repositório piloto para Testes de Unidade.

## [google/guava](https://github.com/google/guava)

Google Guava é um conjunto de bibliotecas que auxiliam o desenvolvimento de aplicações Java. Esta versão possui código aberto, criado principalmente por engenheiros do Google, e são usadas em quase todos os programas Java da empresa.

#### Método testValueEqualityNotInstanceEquality() da classe [TypeTokenTest.java](https://github.com/google/guava/blob/master/guava-tests/test/com/google/common/reflect/TypeTokenTest.java)

A classe TypeTokenTest.java é responsável por TypeToken.java. Nesta classe, temos o método testValueEqualityNotInstanceEquality() que testa se os valores de dois objetos instanciados de uma mesma classe são idênticos, sem verificar se as instâncias são iguais. O teste desse método é o seguinte:

```java
@Test
  public void testValueEqualityNotInstanceEquality() {
    TypeToken<List<String>> a = new TypeToken<List<String>>() {};
    TypeToken<List<String>> b = new TypeToken<List<String>>() {};
    assertEquals(a, b);
  } 
```
 Observe que o método cria duas variáveis, a e b, do mesmo tipo TypeToken<List<String>> e instancia cada uma delas através do comando new TypeToken<List<String>>() {}. Em seguida, ele verifica se os valores de a e b são iguais através da função assertEquals(). Como ambos possuem uma lista de strings vazia a função irá retornar verdadeiro.    
  
#### Método testTrimToSize() da classe [ArrayListMultimapTest.java](https://github.com/google/guava/blob/master/guava-tests/test/com/google/common/collect/ArrayListMultimapTest.java)

A classe ArrayListMultimapTest.java é responsável por ArrayListMultimap.java. Nesta classe, temos o método testTrimToSize() que testa a quantidade de chaves armazenadas e verifica seus valores. O teste desse método é o seguinte:

```java
@Test
  public void testTrimToSize() {
    ArrayListMultimap<String, Integer> multimap = ArrayListMultimap.create();
    multimap.put("foo", 1);
    multimap.put("foo", 2);
    multimap.put("bar", 3);
    multimap.trimToSize();
    assertEquals(3, multimap.size());
    assertThat(multimap.get("foo")).containsExactly(1, 2).inOrder();
    assertThat(multimap.get("bar")).contains(3);
  } 
```
De início, cria-se uma lista vazia do tipo ArrayListMultimap, insere a chave "foo" com os valores 1 e 2, adiciona a chave "bar" com o valor 3 e define o limite de verificação. Posteriormente, testa se a lista possui três valores, o que é verdade. Em seguida, testa se a chave "foo" contém exatamente os valores 1 e 2 nessa ordem, o teste passa. Por fim, testa se a chave "bar" possui valor 3, o que é correto. 

#### Método directedGraph() da classe [ValueGraphTest.java](https://github.com/google/guava/blob/master/guava-tests/test/com/google/common/graph/ValueGraphTest.java)

A classe ValueGraphTest.java é responsável por ValueGraph.java. Nesta classe, temos o método directedGraph() que testa se um grafo é direcionado. O teste desse método é o seguinte:

```java
@Test
  public void directedGraph() {
    graph = ValueGraphBuilder.directed().allowsSelfLoops(true).build();
    graph.putEdgeValue(1, 2, "valueA");
    graph.putEdgeValue(2, 1, "valueB");
    graph.putEdgeValue(2, 3, "valueC");
    graph.putEdgeValue(4, 4, "valueD");

    assertThat(graph.edgeValueOrDefault(1, 2, null)).isEqualTo("valueA");
    assertThat(graph.edgeValueOrDefault(2, 1, null)).isEqualTo("valueB");
    assertThat(graph.edgeValueOrDefault(2, 3, null)).isEqualTo("valueC");
    assertThat(graph.edgeValueOrDefault(4, 4, null)).isEqualTo("valueD");
    assertThat(graph.edgeValueOrDefault(1, 2, DEFAULT)).isEqualTo("valueA");
    assertThat(graph.edgeValueOrDefault(2, 1, DEFAULT)).isEqualTo("valueB");
    assertThat(graph.edgeValueOrDefault(2, 3, DEFAULT)).isEqualTo("valueC");
    assertThat(graph.edgeValueOrDefault(4, 4, DEFAULT)).isEqualTo("valueD");

    String toString = graph.toString();
    assertThat(toString).contains("valueA");
    assertThat(toString).contains("valueB");
    assertThat(toString).contains("valueC");
    assertThat(toString).contains("valueD");
  } 
```
Inicialmente, um grafo vazio é construído sendo que um nó pode possuir auto-loop. Em seguida, adiciona quatro nós ao grafo (1, 2, 3, e 4), interligando-os da seguinte maneira: nó 1 conecta ao 2 com aresta "valueA", nó 2 conecta ao 1 com aresta "valueB" e, também, ao 3 com aresta "valueC". Finalmente, nó 4 conecta a ele mesmo com aresta "valueD". O segundo bloco de código testa se cada conexão entre os nós possuem arestas iguais aos valores especificados anteriormente. Por fim, converte o grafo em uma String e testa se ele contém as arestas de valores A, B, C e D. 
