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

A classe TestObserverTest.java é responsável por TestObserver.java. Nesta classe, temos o método assertTestObserver() que testa o ciclo de vida de um "observable", composto por métodos que são executados quando ocorre algum evento, quando os eventos são concluídos e quando ocorre algum erro. O teste desse método é o seguinte:

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

A classe NotificationTest.java é responsável por Notification.java. Nesta classe temos o método valueOfOnCompleteIsNull() que testa se o valor de uma notificação é nulo e não possui erros quando o tipo de sinal reativo é onComplete. O teste desse método é o seguinte:

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

#### Método hasObservers() da classe [UnicastSubjectTest.java](https://github.com/ReactiveX/RxJava/blob/3.x/src/test/java/io/reactivex/rxjava3/subjects/UnicastSubjectTest.java)

A classe UnicastSubjectTest.java é responsável por UnicastSubject.java. Nesta classe temos o método hasObservers() que testa se existe um observador para um assunto qualquer. O teste desse método é o seguinte:

```java
@Test
  public void hasObservers() {
    UnicastSubject<Integer> us = UnicastSubject.create();

    assertFalse(us.hasObservers());

    TestObserver<Integer> to = us.test();

    assertTrue(us.hasObservers());

    to.dispose();

    assertFalse(us.hasObservers());
  }
```
A classe UnicastSubject representa um assunto que enfileira eventos até que um único observador se inscreva nele. Inicialmente, uma instância dessa classe é criada e armazenada na variável "us". Então, o método testa se há um observador através de assertFalse(us.hasObservers()), que retorna falso. Depois, cria-se um observador "to" que passa a interagir com o objeto. Assim, ao testar novamente se existe um observador a função assertTrue(us.hasObservers()) retorna verdadeiro. Por último, remove o observador pela função to.dispose() e testa, em seguida, se o objeto não contém observadores, o que é verdade.     

#### Método isBug() da classe [RxJavaPluginsTest.java](https://github.com/ReactiveX/RxJava/blob/3.x/src/test/java/io/reactivex/rxjava3/plugins/RxJavaPluginsTest.java)

A classe RxJavaPluginsTest.java é responsável por RxJavaPlugins.java. Nesta classe temos o método isBug() que testa se um plugin adicionado a biblioteca RxJava possui algum erro. O teste desse método é o seguinte:

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
Observe que, ao injetar um plugin para alguma operação padrão do RxJava o método realiza vários testes em busca de algum erro. No primeiro bloco, quatro testes são executados e validados através da função assertFalse(): RuntimeException, IOException, InterruptedException e InterruptedIOException. Nesta situação, espera-se que todos os valores sejam falsos, caso contrário, o teste não passará. No segundo bloco, mais oito testes são feitos instanciando objetos do tipo  NullPointerException, IllegalArgumentException, IllegalStateException, MissingBackpressureException, ProtocolViolationException, UndeliverableException, CompositeException e OnErrorNotImplementedException. Aqui, utiliza-se a função assertTrue() para verificar se valores são verdadeiros, ou seja, que nenhum erro foi identificado.

## [SeleniumHQ/selenium](https://github.com/SeleniumHQ/selenium)

Selenium é uma estrutura gratuita de testes automatizados usada para validar aplicativos da web em diferentes navegadores e plataformas, proporcionando aos desenvolvedores entregar ciclos de testes mais rapidamente.

#### Método testElementImplementsWrapsDriver() da classe [WebElementTest.java](https://github.com/SeleniumHQ/selenium/blob/trunk/java/client/test/org/openqa/selenium/WebElementTest.java)

A classe WebElementTest.java é responsável por WebElement.java. Nesta classe, temos o método testElementImplementsWrapsDriver() que testa se um elemento está implementado no código fonte de uma página. O teste desse método é o seguinte:

```java
@Test
  public void testElementImplementsWrapsDriver() {
    driver.get(pages.simpleTestPage);
    WebElement parent = driver.findElement(By.id("containsSomeDiv"));
    assertThat(parent).isInstanceOf(WrapsDriver.class);
  }
```
Primeiramente, uma página web "simpleTestPage" é aberta de forma automática pelo comando driver.get(). Depois, cria-se a variável "parent" do tipo WebElement, que representa um elemento DOM, e atribui à ela o de identificação "containsSomeDiv". A função driver.findElement() é responsável por procurar na página aberta o elemento correspondente. Então, o método testa se este elemento é uma instância de WrapsDriver.class, ou seja, se ele está presente na página, atraveś da chamada assertThat(). Como "simpleTestPage" refere-se a uma página previamente existente na estrutura, o elemento será localizado e o teste passará. 

#### Método testCleanFileInput() da classe [UploadTest.java](https://github.com/SeleniumHQ/selenium/blob/trunk/java/client/test/org/openqa/selenium/UploadTest.java)

A classe UploadTest.java é responsável por Upload.java. Nesta classe, temos o método testCleanFileInput() que testa se o conteúdo de um campo para envio de arquivos está vazio. O teste desse método é o seguinte:

```java
@Test
  public void testCleanFileInput() {
    driver.get(pages.uploadPage);
    WebElement element = driver.findElement(By.id("upload"));
    element.sendKeys(testFile.getAbsolutePath());
    element.clear();
    assertThat(element.getAttribute("value")).isEqualTo("");
  }
```
De início, o método solicita a abertura da página web "uploadPage" através da função driver.get(). Em seguida, armazena na variável "element", do tipo WebElement, o elemento contido nesta página que possui identificador "upload". Então, escreve automaticamente neste campo, usando o método sendKeys(), o nome do caminho absoluto de um arquivo pertencente a classe "testFile". Após preenchido, o mesmo elemento é esvaziado ao executar o comando element.clear() e testado se ele está realmente vazio após esta opração, utilizando-se da função assertThat() que verifica se o valor do atributo de "element" é igual a "".

#### Método testShouldAllowTheUserToTellIfAnElementIsDisplayedOrNot() da classe [VisibilityTest.java](https://github.com/SeleniumHQ/selenium/blob/trunk/java/client/test/org/openqa/selenium/VisibilityTest.java)

A classe VisibilityTest.java é responsável por Visibility.java. Nesta classe, temos o método testShouldAllowTheUserToTellIfAnElementIsDisplayedOrNot() que testa se um elemento deve ser exibido ou não para o usuário final. O teste desse método é o seguinte:

```java
@Test
  public void testShouldAllowTheUserToTellIfAnElementIsDisplayedOrNot() {
    driver.get(pages.javascriptPage);

    assertThat(driver.findElement(By.id("displayed")).isDisplayed()).isTrue();
    assertThat(driver.findElement(By.id("none")).isDisplayed()).isFalse();
    assertThat(driver.findElement(By.id("suppressedParagraph")).isDisplayed()).isFalse();
    assertThat(driver.findElement(By.id("hidden")).isDisplayed()).isFalse();
  }
```
Observe que, a chamada da função driver.get() abre automaticamente a página de conteúdo javascript "javascriptPage". Com a página aberta inicia-se quatro testes utilizando o comando assertThat(). No primeiro, localiza-se o elemento de identificador "displayed" e verifica se ele está visível para o usuário. No segundo, confirma que o elemento de id "none" está oculto na página. Da mesma maneira, para o terceiro e quarto testes, é analisado se os elementos "suppressedParagraph" e "hidden", respectivamente, estão ocultos para o usuário final. Como a página pertence a estrutura do framework todos os testes devem passar.

#### Método testCanClickOnAnElementWithTopSetToANegativeNumber() da classe [ClickTest.java](https://github.com/SeleniumHQ/selenium/blob/trunk/java/client/test/org/openqa/selenium/VisibilityTest.java)

A classe ClickTest.java é responsável por Click.java. Nesta classe, temos o método testCanClickOnAnElementWithTopSetToANegativeNumber() que testa se um elemento da página foi acionado (clicado) pelo usuário final. O teste desse método é o seguinte:

```java
@Test
  public void testCanClickOnAnElementWithTopSetToANegativeNumber() {
    String page = appServer.whereIs("styledPage.html");
    driver.get(page);
    WebElement searchBox = driver.findElement(By.name("searchBox"));
    searchBox.sendKeys("Cheese");
    driver.findElement(By.name("btn")).click();

    String log = driver.findElement(By.id("log")).getText();
    assertThat(log).isEqualTo("click");
  }
```
Inicialmente, atribui-se à variável "page" o caminho de "styledPage.html". Em seguida, esta página é aberta pela função driver.get(). Depois, localiza-se o elemento de nome "searchBox" e o atribui à variável "searchBox", um WebElement. Após, escreve automaticamente neste elemento a palavra "Cheese", usando a função sendKeys(). Então, o método procura pelo elemento de nome "btn" e o aciona através do evento click(). Para validar esta operação, o texto do elemento de id "log" é armazenado na variável "log", do tipo String. Dessa forma, usa-se a função assertThat() para assegurar que seu conteúdo é a palavra "click", referente à ação proposta.
