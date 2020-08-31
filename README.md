# testes-unidade
Repositório piloto para Testes de Unidade.

## [google/guava](https://github.com/google/guava)

##### [ValueGraphTest.java](https://github.com/google/guava/blob/master/guava-tests/test/com/google/common/graph/ValueGraphTest.java)

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
 O método acima testa se um grafo é direcionado. Inicialmente, ele constrói um grafo vazio no qual um nó pode possuir auto-loop. Em seguida, adiciona quatro nós ao grafo (1, 2, 3, e 4), interligando-os da seguinte maneira: nó 1 conecta ao 2 com aresta "valueA", nó 2 conecta ao 1 com aresta "valueB" e, também, ao 3 com aresta "valueC". Finalmente, nó 4 conecta a ele mesmo com aresta "valueD". O segundo bloco de código testa se cada conexão entre os nós possuem arestas iguais aos valores especificados anteriormente. Por fim, converte o grafo em uma String e testa se ele contém as arestas de valores A, B, C e D. 
