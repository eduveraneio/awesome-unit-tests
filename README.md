# awesome-unit-tests
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

#### Método testConcatVarargs() da classe [FluentIterableTest.java](https://github.com/google/guava/blob/master/guava-tests/test/com/google/common/collect/FluentIterableTest.java)

A classe FluentIterableTest.java é responsável por FluentIterable.java. Nesta classe, temos o método testConcatVarargs() que testa a concatenação dos argumentos de variáveis. O teste desse método é o seguinte:

```java
@Test
  public void testConcatVarargs() {
    List<Integer> list1 = newArrayList(1);
    List<Integer> list2 = newArrayList(4);
    List<Integer> list3 = newArrayList(7, 8);
    List<Integer> list4 = newArrayList(9);
    List<Integer> list5 = newArrayList(10);
    @SuppressWarnings("unchecked")
    FluentIterable<Integer> result = FluentIterable.concat(list1, list2, list3, list4, list5);
    assertEquals(asList(1, 4, 7, 8, 9, 10), newArrayList(result));
    assertEquals("[1, 4, 7, 8, 9, 10]", result.toString());
  } 
```
Perceba que, cinco listas são criadas: list1, list2, list3, list4 e list5. Cada lista dessa é um vetor de inteiros que possui 1 ou mais elementos. A linha que contém o código @SuppressWarnings("unchecked") significa que avisos do tipo "unchecked" serão ignorados. Em seguida, elas são concatenadas através da função "concat" do objeto FluentIterable (que fornece uma interface rica para manipular instâncias Iterable de maneira encadeada) e armazenadas na variável "result". Posteriormente, o método testa se a lista de tamanho fixo asList(1, 4, 7, 8, 9, 10) é igual ao vetor concatenado newArrayList(result), o que é verdade. Além disso, verifica se o vetor [1, 4, 7, 8, 9, 10] é exatamente a saída de "result" convertido para String, o que também é verdadeiro.

#### Método testCycleOfOneWithRemove() da classe [IteratorsTest.java](https://github.com/google/guava/blob/master/guava-tests/test/com/google/common/collect/IteratorsTest.java)

A classe IteratorsTest.java é responsável por Iterators.java. Nesta classe, temos o método testCycleOfOneWithRemove() que testa as iterações de uma lista com um elemento, e quando este elemento é removido. O teste desse método é o seguinte:

```java
@Test
  public void testCycleOfOneWithRemove() {
    Iterable<String> iterable = Lists.newArrayList("a");
    Iterator<String> cycle = Iterators.cycle(iterable);
    assertTrue(cycle.hasNext());
    assertEquals("a", cycle.next());
    cycle.remove();
    assertEquals(Collections.emptyList(), iterable);
    assertFalse(cycle.hasNext());
  }
```
Note que, uma lista de Strings é criada com um único elemento "a" e atribuída a variável "iterable". Após, a variável "cycle" é inicializada e retorna um iterador que irá percorrer indefinidamente os elementos desta lista, desde seu início. O método, então, testa se a lista possui um próximo elemento através do comando assertTrue(cycle.hasNext()), que retorna verdadeiro. Em seguida, verifica se o elemento é exatamente o valor "a", o que também é verdade. Na outra etapa, remove este elemento e testa se a lista está vazia, comparando-a com o método emptyList() do objeto Collections. Como esta validação procede, ou seja, a lista está vazia, testa se ela possui um próximo elemento, no qual o resultado será falso. 

## [ReactiveX/RxJava](https://github.com/ReactiveX/RxJava)

RxJava é uma implementação Java VM de Reactive Extensions: uma biblioteca para compor programas assíncronos e baseados em eventos usando sequências observáveis, possibilitando o uso da programação reativa para Java.

#### Método assertTestObserver() da classe [TestObserverTest.java](https://github.com/ReactiveX/RxJava/blob/3.x/src/test/java/io/reactivex/rxjava3/observers/TestObserverTest.java)

A classe TestObserverTest.java extende a classe RxJavaTest.java e é responsável por TestObserver.java. Nesta classe, temos o método assertTestObserver() que testa o ciclo de vida de um "observable", composto por métodos que são executados quando ocorre algum evento, quando os eventos são concluídos e quando ocorre algum erro. O teste desse método é o seguinte:

```java
@Test
  public void assertTestObserver() {
     Flowable<Integer> oi = Flowable.fromIterable(Arrays.asList(1, 2));
     TestSubscriber<Integer> subscriber = new TestSubscriber<>();
     oi.subscribe(subscriber);

     subscriber.assertValues(1, 2);
     subscriber.assertValueCount(2);
     subscriber.assertComplete().assertNoErrors();
  } 
```
No ínicio, cria-se uma variável "oi" do tipo Flowable, na qual um Observable está emitindo alguma quantidade de dados: um vetor de inteiros com os elementos 1 e 2. Em seguida, cria uma instância de TestSubscriber, atribui à variável "subscriber" e a invoca em "oi". Posteriormente, testa se os valores 1 e 2 estão presentes em "subscriber" através da função assertValues(), que retornará verdadeiro. Depois, testa se este objeto contém exatamente dois elementos, sendo esta afirmação verdade. Por fim, verifica se o evento foi concluído sem a presença de erros, o que também é verdadeiro.
 
#### Método customScheduleDirectDisposed() da classe [SchedulerTest.java](https://github.com/ReactiveX/RxJava/blob/3.x/src/test/java/io/reactivex/rxjava3/schedulers/SchedulerTest.java)

A classe SchedulerTest.java é responsável por Scheduler.java. Nesta classe temos o método customScheduleDirectDisposed() que testa o agendamento personalisado da tarefa, sendo que ela pode ser descatada diretamente. O teste desse método é o seguinte:

```java
@Test
  public void customScheduleDirectDisposed() {
    CustomScheduler scheduler = new CustomScheduler();

    Disposable d = scheduler.scheduleDirect(Functions.EMPTY_RUNNABLE, 1, TimeUnit.MINUTES);

    assertFalse(d.isDisposed());

    d.dispose();

    assertTrue(d.isDisposed());
  } 
```
Temos na primeira linha uma instância de CustomScheduler() sendo armazenada na variável "scheduler", ou seja, inicia-se uma agenda customizada. Em seguida, agenda a execução da tarefa vazia com o atraso de tempo determinado em 1 minuto e atruibui à variável "d", do tipo Disposable. Então, o método testa se a tarefa é descartável através da função assertFalse(), que retorna falso porque a tarefa está agendada. Posteriormente, ela é cancelada quando a função dispose() é requerida e, por fim, testa-se se a tarefa pode ser descartada utilizando a função assertTrue(), que retorna verdadeiro.

#### Método valueOfOnCompleteIsNull() da classe [NotificationTest.java](https://github.com/ReactiveX/RxJava/blob/3.x/src/test/java/io/reactivex/rxjava3/core/NotificationTest.java)

A classe NotificationTest.java extende RxJavaTest.java é responsável por Notification.java. Nesta classe temos o método valueOfOnCompleteIsNull() que testa se o valor de uma notificação é nulo e não possui erros quando o tipo de sinal reativo é onComplete. O teste desse método é o seguinte:

```java
@Test
  public void valueOfOnCompleteIsNull() {
    Notification<Integer> notification = Notification.createOnComplete();

    assertNull(notification.getValue());
    assertNull(notification.getError());
    assertTrue(notification.isOnComplete());
  }
```
Uma notificação representa um dos três tipos de sinais reativos: onNext, onError e onComplete e mantém seus valores de parâmetro (um valor, um Throwable, nada). Perceba que, inicialmente, uma notificação onComplete é criada através da função createOnComplete() e armazenada na variável "notification" do tipo Notification. O método, então, testa se este valor é nulo e também verifica se não possui algum erro através da chamada de funções assertNull(). Em ambos os casos, o valor retornado será nulo, logo, o teste passará. Após isto, o método verifica se o objeto notification é onComplete, o que é verdade.  

#### Método isBug() da classe [RxJavaPluginsTest.java](https://github.com/ReactiveX/RxJava/blob/3.x/src/test/java/io/reactivex/rxjava3/plugins/RxJavaPluginsTest.java)

A classe RxJavaPluginsTest.java extende RxJavaTest.java é responsável por RxJavaPlugins.java. Nesta classe temos o método isBug() que testa se um plugin adicionado a biblioteca RxJava possui algum erro. O teste desse método é o seguinte:

```java
@Test
  public void isBug() {
    assertFalse(RxJavaPlugins.isBug(new RuntimeException()));
    assertFalse(RxJavaPlugins.isBug(new IOException()));
    assertFalse(RxJavaPlugins.isBug(new InterruptedException()));
    assertFalse(RxJavaPlugins.isBug(new InterruptedIOException()));

    assertTrue(RxJavaPlugins.isBug(new NullPointerException()));
    assertTrue(RxJavaPlugins.isBug(new IllegalArgumentException()));
    assertTrue(RxJavaPlugins.isBug(new IllegalStateException()));
    assertTrue(RxJavaPlugins.isBug(new MissingBackpressureException()));
    assertTrue(RxJavaPlugins.isBug(new ProtocolViolationException("")));
    assertTrue(RxJavaPlugins.isBug(new UndeliverableException(new TestException())));
    assertTrue(RxJavaPlugins.isBug(new CompositeException(new TestException())));
    assertTrue(RxJavaPlugins.isBug(new OnErrorNotImplementedException(new TestException())));
  }
```
Observe que, ao injetar um plugin para alguma operação padrão do RxJava o método realiza vários testes em busca de algum erro. No primeiro bloco, quatro testes são executados e validados através da função assertFalse(): RuntimeException, IOException, InterruptedException e InterruptedIOException. Nesta situação, espera-se que todos os valores sejam falsos, caso contrário, o teste não passará. No segundo bloco, mais oito testes são feitos instanciando objetos do tipo  NullPointerException, IllegalArgumentException, IllegalStateException, MissingBackpressureException, ProtocolViolationException, UndeliverableException, CompositeException e OnErrorNotImplementedException. Aqui, utiliza-se a função assertTrue() para verificar se valores são verdadeiros, ou seja, que nenhuma erro foi identificado para as instãncias solicitadas.
