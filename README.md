# Clean Code PHP

## Clean Code concepts adapted for PHP
> O livro Software engineering principles, de Robert C. Martin Clean Code, adaptado para PHP. Isso não é um guia de estilo. É um guia para podução de software em PHP legível, reusável, e refatorável.

## Sumário

  1. [Introdução](#introdução)
  2. [Geral](#geral)
     * [Use as tags de abertura e fechamento adequadas](#use-as-tags-de-abertura-e-fechamento-adequadas)
     * [Comente apenas o necessário](#comente-apenas-o-necessário)
  3. [Variáveis](#variáveis)
     * [Use variáveis pronunciáveis e com significado claro](#use-variáveis-pronunciaveis-e-com-significado-claro)
     * [Use o mesmo vocabulário para o mesmo tipo de variável](#use-o-mesmo-vocabulário-para-o-mesmo-tipo-de-variável)
     * [Use nomes pesquisáveis (parte 1)](#use-nomes-pesquisáveis-parte-1)
     * [Use nomes pesquisáveis (parte 2)](#use-nomes-pesquisáveis-parte-2)
     * [Use nomes explicativos](#use-nomes-explicativos)
     * [Evite mapa mental](#evite-mapa-mental)
     * [Não coloque contexto desnecessário](#não-coloque-contexto-desnecessário)
     * [Use argumentos padrão ao invéis de condicionais](#use-argumentos-padrão-ao-invéis-de-condicionais)
     * [Evite ao máximo variáveis desnecessárias](#evite-ao-máximo-variáveis-desnecessárias)
     * [Não use abreviações](#nao-use-abreviacoes)
  4. [Funções](#funções)
     * [Parâmetros de funções (2 ou menos)](#parâmetros-de-funções-2-ou-menos)
     * [Funções devem fazer apenas uma coisa](#funções-devem-fazer-apenas-uma-coisa)
     * [Use type hinting para parâmetros de método](#use-type-hinting-para-parâmetros-de-método)
     * [Nome de função deve dizer o que ela faz](#nome-de-função-deve-dizer-o-que-ela-faz)
     * [Funções devem ter apenas um nível de abstração](#funções-devem-ter-apenas-um-nível-de-abstração)
     * [Utilize o padrão de return early para funções](#utilize-o-padrão-de-return-early-para-funções)
     * [Não use flags como parâmetros](#não-use-flags-como-parâmetros)
     * [Evite efeito colateral](#evite-efeito-colateral)
     * [Não escreva funções globais](#não-escreva-funções-globais)
     * [Não use o padrão Singleton](#não-use-o-padrão-singleton)
     * [Encapsule condicionais](#encapsule-condicionais)
     * [Evite condicionais negativas](#evite-condicionais-negativas)
     * [Evite condicionais](#evite-condicionais)
     * [Evite verificação de tipo (parte 1)](#evite-verificação-de-tipo-parte-1)
     * [Evite verificação de tipo (parte 2)](#evite-verificação-de-tipo-parte-2)
     * [Remova código morto](#remova-código-morto)
  5. [Objetos e estrutura de dados](#objetos-e-estrutura-de-dados)
     * [Use getters e setters](#use-getters-e-setters)
     * [Faça objetos terem membros private/protected](#faça-objetos-terem-membros-privateprotected)
  6. [Classes](#classes)
     * [S: Princípio da Responsabilidade Única (SRP)](#princípio-da-responsabilidade-Única-srp)
     * [O: Princípio do Aberto/Fechado (OCP)](#princípio-do-abertofechado-ocp)
     * [L: Princício da Substituição de Liskov (LSP)](#princício-da-substituição-de-liskov-lsp)
     * [I: Princípio da Segregação de interface (ISP)](#princípio-da-segregação-de-interface-isp)
     * [D: Princípio da Injeção de dependências (DIP)](#princípio-da-injeção-de-dependências-dip)
     * [Use method chaining](#use-method-chaining)
     * [Prefira composição do que herança](#prefira-composição-do-que-herança)
  7. [Não repita você mesmo (DRY)](#não-repita-você-mesmo)
  8. [Traduções](#traduções)

## Introdução

O livro Software engineering principles, de Robert C. Martin
[*Clean Code*](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882),
adaptado para PHP. Isso não é um guia de estilo. É um guia para podução de software em PHP legível,
reusável, e refatorável.

Nem todos os princípios aqui contidos devem ser rigorosamente seguidos, e muito menos serão 
universalmente acordados. Estas são orientações e nada mais, mas são codificadas em muitos
anos de experiência coletiva pelos autores do *Clean Code*.

* "Código limpo sempre parece que foi escrito por alguém que se importa". Michael Feathers
* "Você sabe que está trabalhando em um código limpo quando cada rotina que você lê acaba sendo exatamente o que você espera". Ward Cunningham
* "Qualquer tolo pode escrever um código que o computador possa entender. Bons programadores escrevem códigos que humanos possam entender". Martin Fowler 

## Geral

### Use as tags de abertura e fechamento adequadas

Utilize as tags `<?php ?>` no lugar de `<? ?>`. Na maioria das vezes os desenvolvedores adoram atalhos e simplificações de implementações como o `short tags` do PHP. Evite isso! Uma boa IDE deve ser capaz de lhe ajudar com o auto-complete nesses casos não havendo desculpa para tal.
Lembre-se que o `short tags sintax` não vem habilitado no arquivo `php.ini` por padrão e você deve efetuar a configuração manualmente para um correto funcionamento quando utilizado desse recurso.

**Ruim**
```php
<?
  echo "Hello world";
?>
 
<?="Hello world"; ?>
```

**Bom**
```php
<?php 
  echo 'Hello world';
?>

<?php echo 'Hello world'; ?>
```

**[#voltar para o topo](#sumário)**

### Comente apenas o necessário

Esse princípio afirma que comentários podem ser feitos, porém, se forem realmente necessários. Segundo Uncle Bob, os comentários mentem. E isso tem uma explicação lógica.

O que ocorre é que, enquanto os códigos são constantemente modificados, os comentários não. Eles são esquecidos e, portanto, deixam de retratar a funcionalidade real dos códigos.

Logo, se for para comentar, que seja somente o necessário e que seja revisado juntamente com o código que o acompanha.

**Ruim:**

```php
/** Get the user details */
public function getUser(int $id)
{
  /** Fetch the user details by id */
  $user = User::where('id', $id)->first();

  /** Calling function to calculate user's current month salary */
  $this->currentMonthSalary($user);
  
  /** return the user */
  return $user;
}

/** Calculating the current month salary of user */
private function currentMonthSalary(User $user)
{
  /** Salary = (Total Days - Leave Days) * PerDay Salary */
  // ...
}
```

**Bom:**

```php
public function getUser(int $id)
{
  $user = User::where('id', $id)->first();

  $this->currentMonthSalary($user);

  return $user;
}

private function currentMonthSalary(User $user)
{
  /** Salary = (Total Days - Leave Days) * PerDay Salary */
  // ...
}
```

**[#voltar para o topo](#sumário)**

## Variáveis

### Use variáveis pronunciáveis e com significado claro

**Ruim:**

```php
$ymdstr = $date->format('y-m-d');
```

**Bom:**

```php
$currentDate = $date->format('y-m-d');
```

**[#voltar para o topo](#sumário)**

### Use o mesmo vocabulário para o mesmo tipo de variável

**Ruim:**

```php
getUserInfo();
getUserData();
getUserRecord();
getUserProfile();
```

**Bom:**

```php
getUser();
```

**[#voltar para o topo](#sumário)**

### Use nomes pesquisáveis (parte 1)

Nós vamos ler mais código do que escrever. É importante que o código que nós escrevemos seja
legível e pesquisável. Por *não* nomear variáveis que sejam significativas para o entendimento
do nosso programa, nós machucamos nossos "leitores".
Escreva variáveis com nomes pesquisáveis.

**Ruim:**

```php
// O que diabos é 448?
$result = $serializer->serialize($data, 448);
```

**Bom:**

```php
$json = $serializer->serialize($data, JSON_UNESCAPED_SLASHES | JSON_PRETTY_PRINT | JSON_UNESCAPED_UNICODE);
```

### Use nomes pesquisáveis (parte 2)

**Ruim:**

```php
// O que diabos é 4?
if ($user->access === 4) {
    // ...
}
```

**Bom:**

```php
class User
{
    const ACCESS_READ = 1;
    const ACCESS_CREATE = 2;
    const ACCESS_UPDATE = 4;
    const ACCESS_DELETE = 8;
}

if ($user->access === User::ACCESS_UPDATE) {
    // faça a edição ...
}
```

**[#voltar para o topo](#sumário)**

### Use nomes explicativos

**Ruim:**

```php
$address = 'One Infinite Loop, Cupertino 95014';
$cityZipCodeRegex = '/^[^,\\]+[,\\\s]+(.+?)\s*(\d{5})?$/';
preg_match($cityZipCodeRegex, $address, $matches);

saveCityZipCode($matches[1], $matches[2]);
```

**Nada mal:**

É melhor, mas ainda depende do regex.

```php
$address = 'One Infinite Loop, Cupertino 95014';
$cityZipCodeRegex = '/^[^,\\]+[,\\\s]+(.+?)\s*(\d{5})?$/';
preg_match($cityZipCodeRegex, $address, $matches);

list(, $city, $zipCode) = $matches;
saveCityZipCode($city, $zipCode);
```

**Bom:**

Diminui a dependência do regex nomeando os subpadrões.

```php
$address = 'One Infinite Loop, Cupertino 95014';
$cityZipCodeRegex = '/^[^,\\]+[,\\\s]+(?<city>.+?)\s*(?<zipCode>\d{5})?$/';
preg_match($cityZipCodeRegex, $address, $matches);

saveCityZipCode($matches['city'], $matches['zipCode']);
```

**[#voltar para o topo](#sumário)**

### Evite mapa mental

Nada favorece o leitor do seu código traduzir o que as variáveis significam.
Explícito é melhor que implicito.

**Ruim:**

```php
$l = ['Austin', 'New York', 'San Francisco'];

for ($i = 0; $i < count($l); $i++) {
    $li = $l[$i];
    doStuff();
    doSomeOtherStuff();
    // ...
    // ...
    // ...
    // Espere, o que é `$li` mesmo?
    dispatch($li);
}
```

**Bom:**

```php
$locations = ['Austin', 'New York', 'San Francisco'];

foreach ($locations as $location) {
    doStuff();
    doSomeOtherStuff();
    // ...
    // ...
    // ...
    dispatch($location);
}
```

**[#voltar para o topo](#sumário)**

### Não coloque contexto desnecessário

Se o nome de sua classe/objeto diz alguma coisa, não repita no nome de suas propriedades.

**Ruim:**

```php
class Car
{
    public $carBrand;
    public $carModel;
    public $carColor;

    //...
}
```

**Bom:**

```php
class Car
{
    public $brand;
    public $model;
    public $color;

    //...
}
```

**[#voltar para o topo](#sumário)**

### Use argumentos padrão ao invés de condicionais

**Nada mal:**

Isso não é nada mal porque `$breweryName` pode ser `NULL`.

```php
function createMicrobrewery($breweryName = 'Hipster Brew Co.')
{
    // ...
}
```

**Nada mal:**

Isso pode ser entendido melhor do que a versão anterior, mas é melhor ter o controle do valor da sua variável.

```php
function createMicrobrewery($name = null)
{
    $breweryName = $name ?: 'Hipster Brew Co.';
    // ...
}
```

**Bom:**

Se você tiver suporte para PHP 7+, você pode usar [type hinting](http://php.net/manual/en/functions.arguments.php#functions.arguments.type-declaration) e ter certeza que
`$breweryName` não será `NULL`.

```php
function createMicrobrewery(string $breweryName = 'Hipster Brew Co.')
{
    // ...
}
```

**[#voltar para o topo](#sumário)**

### Evite ao máximo variáveis desnecessárias

Basicamente, se você utiliza a variável mais de 2 vezes em um código, mantenha essa variável, caso contrário, use-a diretamente dentro do código. Isso melhora a legibilidade e torna seu código muito mais limpo.

**Ruim**
```php
public function create()
{
    $zones = Zone::get();

    $data = [
        'zones' => $zones,
    ];

    return view('customer.create', [
        'data' => $data
    ]);
} 
```

**Bom**
```php
public function create()
{
    return view('customer.create', [
        'zones' => Zone::get()
    ]);
} 
```

**[#voltar para o topo](#sumário)**

### Não use abreviações

Abreviações nada mais são do que palavras que você basicamente usa em mensagens de texto, só. Nada favorece o leitor do seu código traduzir o que as variáveis significam colaborando com o mapeamento mental.

**Ruim:**

```php
$d = [...];

$ord = Order::create($d);
// ...
$ord->notify();
```

**Bom:**

```php
$orderData = [...];

$order = Order::create($orderData);
// ...
$order->notify();
```

**[#voltar para o topo](#sumário)**

## Funções

Para estruturar um código limpo, é necessário criar funções simples, pequenas e claras. Segundo Robert, as duas regras principais das funções são as seguintes:

1) Elas precisam ser pequenas
2) Elas precisam de ser ainda menores

### Parâmetros de funções (2 ou menos)

Limitando a quantidade de parâmetros em uma função é importante porque é possivel testar
a função de forma mais fácil. Tendo mais de três conduz em uma explosão combinacional
onde você tem vários casos de teste de diferentes parâmetros separados.

Zero parâmetros é o caso ideal. Um ou dois parâmetros é ok, e três ou mais deve ser evitado.
Qualquer coisa mais deve ser consolidado. Frequentemente, se você tem mais de dois parâmetros
quer dizer que sua função está tentando fazer coisas demais. Em casos onde não está, 
você deve usar um objeto higher-level para suprir os parâmetros.

**Ruim:**

```php
function createMenu($title, $body, $buttonText, $cancellable)
{
    // ...
}
```

**Bom:**

```php
class MenuConfig
{
    public $title;
    public $body;
    public $buttonText;
    public $cancellable = false;
}

$config = new MenuConfig();
$config->title = 'Foo';
$config->body = 'Bar';
$config->buttonText = 'Baz';
$config->cancellable = true;

function createMenu(MenuConfig $config)
{
    // ...
}
```

**[#voltar para o topo](#sumário)**

### Funções devem fazer apenas uma coisa

Esse é de longe a regra mais importante na engenharia de software. Quando funções fazem
mais do que uma coisa, elas são difíceis de utilizar, testar e racionalizar. Quando você
pode isolar uma função para apenas uma coisa, elas podem ser refatoradas facilmente e seu 
código será lido com muito mais clareza. Se você não pegar nada desse guia, além disso,
você vai está à frente de muitos desenvolvedores.

**Ruim:**
```php
function emailClients($clients)
{
    foreach ($clients as $client) {
        $clientRecord = $db->find($client);
        if ($clientRecord->isActive()) {
            email($client);
        }
    }
}
```

**Bom:**

```php
function emailClients($clients)
{
    $activeClients = activeClients($clients);
    array_walk($activeClients, 'email');
}

function activeClients($clients)
{
    return array_filter($clients, 'isClientActive');
}

function isClientActive($client)
{
    $clientRecord = $db->find($client);

    return $clientRecord->isActive();
}
```

**[#voltar para o topo](#sumário)**

### Use type hinting para parâmetros de método

Basicamente, o parâmetro que você usa com os métodos será interpretado de forma diferente por diferentes usuários.

Portanto, se você usar Type Hinting, isso ajudará os usuários a lerem seu código, até mesmo sua IDE interpretará o hint e tentará completar automaticamente, e o PHP lançará erros e avisos apropriados no mesmo.

**Ruim**

Aqui não sabemos se o parâmetro `$user` é um inteiro, array, objeto ou qualquer outro tipo

```php
public function show($user)
{
    // ...
}
```

**Bom**

```php
public function show(User $user)
{
    // ...
}
```

```php
public function schoolFunction(array $guests)
{
    // ...
}
```

**[#voltar para o topo](#sumário)**

### Nome de função deve dizer o que ela faz

O nome das função ou método deve ser claro em relação ao seu objetivo / ação.

**Ruim:**

```php
class Email
{
    //...

    public function handle()
    {
        mail($this->to, $this->subject, $this->body);
    }
}

$message = new Email(...);
// O que é isso? Um identificador para a mensagem? Estamos gravando em um arquivo agora?
$message->handle();
```

**Bom:**

```php
class Email 
{
    //...

    public function send()
    {
        mail($this->to, $this->subject, $this->body);
    }
}

$message = new Email(...);
// Claro e óbvio
$message->send();
```

**Ruim:**

```php
public function user($email)
{
    // ...
}
```

**Bom:**

```php
public function getUserByEmail($email)
{
    // ...
}
```

**[#voltar para o topo](#sumário)**

### Funções devem ter apenas um nível de abstração

Quando você possui mais de um nível de abstração, sua função deve estar fazendo
coisas demais. Separar as funções leva a reusabilidade e testes de forma
mais fácil.

**Ruim:**

```php
function parseBetterJSAlternative($code)
{
    $regexes = [
        // ...
    ];

    $statements = explode(' ', $code);
    $tokens = [];
    foreach ($regexes as $regex) {
        foreach ($statements as $statement) {
            // ...
        }
    }

    $ast = [];
    foreach ($tokens as $token) {
        // lex...
    }

    foreach ($ast as $node) {
        // parse...
    }
}
```

**Ruim também:**

Cuidamos de algumas funcionalidades, mas a função `parseBetterJSAlternative()`  ainda é muito complexa e não testavel.

```php
function tokenize($code)
{
    $regexes = [
        // ...
    ];

    $statements = explode(' ', $code);
    $tokens = [];
    foreach ($regexes as $regex) {
        foreach ($statements as $statement) {
            $tokens[] = /* ... */;
        }
    }

    return $tokens;
}

function lexer($tokens)
{
    $ast = [];
    foreach ($tokens as $token) {
        $ast[] = /* ... */;
    }

    return $ast;
}

function parseBetterJSAlternative($code)
{
    $tokens = tokenize($code);
    $ast = lexer($tokens);
    foreach ($ast as $node) {
        // parse...
    }
}
```

**Bom:**

A melhor solução é retirar as dependencias da função `parseBetterJSAlternative()`.

```php
class Tokenizer
{
    public function tokenize($code)
    {
        $regexes = [
            // ...
        ];

        $statements = explode(' ', $code);
        $tokens = [];
        foreach ($regexes as $regex) {
            foreach ($statements as $statement) {
                $tokens[] = /* ... */;
            }
        }

        return $tokens;
    }
}

class Lexer
{
    public function lexify($tokens)
    {
        $ast = [];
        foreach ($tokens as $token) {
            $ast[] = /* ... */;
        }

        return $ast;
    }
}

class BetterJSAlternative
{
    private $tokenizer;
    private $lexer;

    public function __construct(Tokenizer $tokenizer, Lexer $lexer)
    {
        $this->tokenizer = $tokenizer;
        $this->lexer = $lexer;
    }

    public function parse($code)
    {
        $tokens = $this->tokenizer->tokenize($code);
        $ast = $this->lexer->lexify($tokens);
        foreach ($ast as $node) {
            // parse...
        }
    }
}
```

**[#voltar para o topo](#sumário)**

### Utilize o padrão de return early para funções

Utilize o padrão `return early` para funções e fluxos mais claros.

**Ruim:**

```php
function isShopOpen($day)
{
    if ($day) {
        return in_array(strtolower($day), ['friday', 'saturday', 'sunday']) ? true : false;
    }else{
        return false;
    }
}
```

**Bom:**

```php
function isShopOpen($day)
{
    if (empty($day)) {
        return false;
    }

    return in_array(strtolower($day), ['friday', 'saturday', 'sunday']) ? true : false;
}
```

**[#voltar para o topo](#sumário)**

### Não use flags como parâmetros

Flags dizem para seu usuário que essa função faz mais de uma coisa. Funções devem
fazer apenas uma coisa. Divida suas funções se elas estão seguindo diferentes
diretórios baseado em um boleano.

**Ruim:**

```php
function createFile($name, $temp = false)
{
    if ($temp) {
        touch('./temp/'.$name);
    } else {
        touch($name);
    }
}
```

**Bom:**

```php
function createFile($name)
{
    touch($name);
}

function createTempFile($name)
{
    touch('./temp/'.$name);
}
```

**[#voltar para o topo](#sumário)**

### Evite efeito colateral

Uma função produz um efeito colateral se ela faz mais do que pegar um valor e retornar
outro ou outros. Um efeito colateral pode ser, escrever em um arquivo, modificar
uma variável global, ou acidentalmente mandar todo seu dinheiro pra um estranho.

Agora, você pode ter efeitos colaterais em uma determinada situação. Como no exemplo
anterior, você pode precisar escrever em um arquivo. O que você quer fazer é centralizar
onde você está fazendo isso. Não tenha várias funções ou classes que escrevem em um
arquivo particular. Tenha um serviço que faça isso. Um e apenas um.

O ponto principal é evitar armadilhas comuns como compartilhar um estado entre objetos
sem qualquer estrutura, usando dados mutáveis que podem ser escritos por qualquer coisa,
e não centralizando onde os efeitos colaterais irão ocorrer. Se você pode fazer isso,
você ficará mais feliz do que a maioria dos outros programadores.

**Ruim:**

```php
// Global variable referenced by following function.
// If we had another function that used this name, now it'd be an array and it could break it.
$name = 'Ryan McDermott';

function splitIntoFirstAndLastName()
{
    global $name;

    $name = explode(' ', $name);
}

splitIntoFirstAndLastName();

var_dump($name); // ['Ryan', 'McDermott'];
```

**Bom:**

```php
function splitIntoFirstAndLastName($name)
{
    return explode(' ', $name);
}

$name = 'Ryan McDermott';
$newName = splitIntoFirstAndLastName($name);

var_dump($name); // 'Ryan McDermott';
var_dump($newName); // ['Ryan', 'McDermott'];
```

**[#voltar para o topo](#sumário)**

### Não escreva funções globais

Criar globais é uma má prática em várias linguagens porque você pode colidir com outra 
biblioteca e não será claro para o usuário de sua API até que ele tenha uma exceção em
produção. Vamos pensar em um exemplo: se você quiser um array de configuração.
Vode poderia escrever uma função global como `config()`, mas pode colidir com outra biblioteca
que tentou fazer a mesma coisa.

**Ruim:**

```php
function config()
{
    return  [
        'foo' => 'bar',
    ]
}
```

**Bom:**

```php
class Configuration
{
    private $configuration = [];

    public function __construct(array $configuration)
    {
        $this->configuration = $configuration;
    }

    public function get($key)
    {
        return isset($this->configuration[$key]) ? $this->configuration[$key] : null;
    }
}
```

Carrega a configuração e crie uma instância da classe `Configuration`

```php
$configuration = new Configuration([
    'foo' => 'bar',
]);
```

Agora você deve usar a instância de `Configuration` na sua aplicação.

**[#voltar para o topo](#sumário)**

### Não use o padrão Singleton

Singleton é um [anti-padrão](https://en.wikipedia.org/wiki/Singleton_pattern). Interpretado de 
Brian Button:
 1. Eles geralmente são usados como uma **instância global**, por que isso é tão ruim? Porque **você esconde as dependencias** da aplicação no seu código, em vez de expor eles através de interfaces. Fazendo alguma coisa global pra evitar que o [código cheire mal](https://en.wikipedia.org/wiki/Code_smell).
 2. Ele viola o [Princípio da Responsabilidade Única](#princípio-da-responsabilidade-Única-srp): pelo fato de **controlar sua própria criação e ciclo de vida**.
 3. Eles inerentemente fazem com que o código seja muito [acoplado](https://en.wikipedia.org/wiki/Coupling_%28computer_programming%29). Isso faz com que eles resultem em falsos resultados em **testes** em muitos casos.
 4. Eles carregam o estado por todo o tempo de vida da aplicação. Um bateria de testes **para simular uma situação específica os testes precisam ser ordenados** deixando o propósito dos testes unitários de lado. Por quê? Porque cada teste unitário deve ser independente um do outro.

Também tem algumas ideias muitos boas do [Misko Hevery](http://misko.hevery.com/about/) falando sobre o [centro do problema](http://misko.hevery.com/2008/08/25/root-cause-of-singletons/).

**Ruim:**

```php
class DBConnection
{
    private static $instance;

    private function __construct($dsn)
    {
        // ...
    }

    public static function getInstance()
    {
        if (self::$instance === null) {
            self::$instance = new self();
        }

        return self::$instance;
    }

    // ...
}

$singleton = DBConnection::getInstance();
```

**Bom:**

```php
class DBConnection
{
    public function __construct(array $dsn)
    {
        // ...
    }

     // ...
}
```

Criar uma instância da classe `DBConnection` e configuar com [DSN](http://php.net/manual/en/pdo.construct.php#refsect1-pdo.construct-parameters).

```php
$connection = new DBConnection($dsn);
```

E agora você deve usar a instância de `DBConnection` na sua aplicação.

**[#voltar para o topo](#sumário)**

### Encapsule condicionais

**Ruim:**

```php
if ($article->state === 'published') {
    // ...
}
```

**Bom:**

```php
if ($article->isPublished()) {
    // ...
}
```

**[#voltar para o topo](#sumário)**

### Evite condicionais negativas

**Ruim:**

```php
function isDOMNodeNotPresent($node)
{
    // ...
}

if (!isDOMNodeNotPresent($node))
{
    // ...
}
```

**Bom:**

```php
function isDOMNodePresent($node)
{
    // ...
}

if (isDOMNodePresent($node)) {
    // ...
}
```

**[#voltar para o topo](#sumário)**

### Evite condicionais

Essa parece ser uma tarefa impossível. A primeira coisa que as pessoas dizem
quando ouvem isso é "como eu poderia fazer qualquer coisa sem um `if`?" A
resposta é que você pode usar polimorfismo para chegar no mesmo resultado em
muitos casos. A segunda pergunta é, "Bom, isso é legal, mas por que eu faria 
isso?" A resposta é um outro conceito de código limpo que nós aprendemos:
Uma função deve fazer apenas uma coisa. Quando você tem classes e funções com
`if`, você está dizendo que sua função faz mais de uma coisa. Lembre-se,
só uma coisa.

**Ruim:**

```php
class Airplane
{
    // ...

    public function getCruisingAltitude()
    {
        switch ($this->type) {
            case '777':
                return $this->getMaxAltitude() - $this->getPassengerCount();
            case 'Air Force One':
                return $this->getMaxAltitude();
            case 'Cessna':
                return $this->getMaxAltitude() - $this->getFuelExpenditure();
        }
    }
}
```

**Bom:**

```php
interface Airplane
{
    // ...

    public function getCruisingAltitude();
}

class Boeing777 implements Airplane
{
    // ...

    public function getCruisingAltitude()
    {
        return $this->getMaxAltitude() - $this->getPassengerCount();
    }
}

class AirForceOne implements Airplane
{
    // ...

    public function getCruisingAltitude()
    {
        return $this->getMaxAltitude();
    }
}

class Cessna implements Airplane
{
    // ...

    public function getCruisingAltitude()
    {
        return $this->getMaxAltitude() - $this->getFuelExpenditure();
    }
}
```

**[#voltar para o topo](#sumário)**

### Evite verificação de tipo (parte 1)

PHP não é fortemente tipado, isso quer dizer, que suas funções podem receber
qualquer tipo de argumento. Algumas vezes você é fisgado pela liberdade
e isso se torna tentador fazer verificação de tipo nas suas funções.
Há várias maneiras de evitar fazer isso. A primeira é, APIs consistentes

**Ruim:**

```php
function travelToTexas($vehicle)
{
    if ($vehicle instanceof Bicycle) {
        $vehicle->peddleTo(new Location('texas'));
    } elseif ($vehicle instanceof Car) {
        $vehicle->driveTo(new Location('texas'));
    }
}
```

**Bom:**

```php
function travelToTexas(Traveler $vehicle)
{
    $vehicle->travelTo(new Location('texas'));
}
```

**[#voltar para o topo](#sumário)**

### Evite verificação de tipo (parte 2)

Se você estiver trabalhando com tipos primitivos como strings, inteiros e arrays,
e você usa PHP 7+ e você não pode usar polimorfismo, mas você ainda sente a necessidade
de verificar os tipos, você deve considerar a [declaração de tipo](http://php.net/manual/en/functions.arguments.php#functions.arguments.type-declaration)
ou modo estrito. Isso permite que você use tipos estáticos por padrão na sintáxe da 
linguagem PHP. O problema com verificação de tipo manual é que isso requer muito mais
código escrito para ter os tipos validados, e você perde a legibilidade do código.
Mantenha seu PHP limpo, escreva bons testes, e tenha boas revisões. Caso contrário, 
faça tudo como o modo estrito do PHP.

**Ruim:**

```php
function combine($val1, $val2)
{
    if (!is_numeric($val1) || !is_numeric($val2)) {
        throw new \Exception('Must be of type Number');
    }

    return $val1 + $val2;
}
```

**Bom:**

```php
function combine(int $val1, int $val2)
{
    return $val1 + $val2;
}
```

**[#voltar para o topo](#sumário)**

### Remova código morto

Código morto é tão ruim quanto duplicar o código. Não há motivos para manter
ele no seu projeto. Se ele não está sendo chamado, livre-se dele! Ele ainda 
está seguro no histórico de versão quando você precisar dele.

**Ruim:**

```php
function oldRequestModule($url)
{
    // ...
}

function newRequestModule($url)
{
    // ...
}

$request = newRequestModule($requestUrl);
inventoryTracker('apples', $request, 'www.inventory-awesome.io');
```

**Bom:**

```php
function requestModule($url)
{
    // ...
}

$request = requestModule($requestUrl);
inventoryTracker('apples', $request, 'www.inventory-awesome.io');
```

**[#voltar para o topo](#sumário)**


## Objetos e estrutura de dados

### Use getters e setters

No PHP, você pode setar as palavaras-chaves `public`, `protected` e `private` para os métodos.
Usando-as, você pode controlar a visibilidade das propriedades em um objeto.

* Quando você deseja fazer mais do que obter uma propriedade de objeto, não tem
  que procurar e alterar todos os acessadores na sua base de código.
* Facilita a adição de validações ao fazer um `set`.
* Encapsula a representação interna.
* Fácil de adicionar registro e tratamento de erros ao obter e configurar.
* Herdando essa classe, você pode substituir a funcionalidade padrão.
* Você pode efetuar o `lazy load` das propriedades do seu objeto, digamos que obtê-lo de um
servidor.

Além disso, isso faz parte do Princípio do Aberto / Fechado, dos princípios de design da orientação a objetos.

**Ruim:**

```php
class BankAccount
{
    public $balance = 1000;
}

$bankAccount = new BankAccount();

// Buy shoes...
$bankAccount->balance -= 100;
```

**Bom:**

```php
class BankAccount
{
    private $balance;

    public function __construct($balance = 1000)
    {
      $this->balance = $balance;
    }

    public function withdrawBalance($amount)
    {
        if ($amount > $this->balance) {
            throw new \Exception('Amount greater than available balance.');
        }

        $this->balance -= $amount;
    }

    public function depositBalance($amount)
    {
        $this->balance += $amount;
    }

    public function getBalance()
    {
        return $this->balance;
    }
}

$bankAccount = new BankAccount();

// Buy shoes...
$bankAccount->withdrawBalance($shoesPrice);

// Get balance
$balance = $bankAccount->getBalance();
```

**[#voltar para o topo](#sumário)**

### Faça objetos terem membros private/protected

**Ruim:**

```php
class Employee
{
    public $name;

    public function __construct($name)
    {
        $this->name = $name;
    }
}

$employee = new Employee('John Doe');
echo 'Employee name: '.$employee->name; // Employee name: John Doe
```

**Bom:**

```php
class Employee
{
    private $name;

    public function __construct($name)
    {
        $this->name = $name;
    }

    public function getName()
    {
        return $this->name;
    }
}

$employee = new Employee('John Doe');
echo 'Employee name: '.$employee->getName(); // Employee name: John Doe
```

**[#voltar para o topo](#sumário)**

## Classes

### Princípio da Responsabilidade Única (SRP)

Conforme declarado no Código Limpo, "Nunca deve haver mais de um motivo para uma classe
mudar ". É tentador compor uma classe com muitas funcionalidades, como
quando você só pode levar uma mala no seu voo. O problema com isso é
que sua classe não será conceitualmente coesa e oferecerá muitas razões para
mudar. Minimizar a quantidade de vezes que você precisa alterar uma classe é importante.
É importante porque, se houver muita funcionalidade em uma classe e você modificar uma parte dela,
pode ser difícil entender como isso afetará outros módulos dependentes do seu código.

**Ruim:**

```php
class UserSettings
{
    private $user;

    public function __construct($user)
    {
        $this->user = $user;
    }

    public function changeSettings($settings)
    {
        if ($this->verifyCredentials()) {
            // ...
        }
    }

    private function verifyCredentials()
    {
        // ...
    }
}
```

**Bom:**

```php
class UserAuth 
{
    private $user;

    public function __construct($user)
    {
        $this->user = $user;
    }
    
    public function verifyCredentials()
    {
        // ...
    }
}

class UserSettings 
{
    private $user;
    private $auth;

    public function __construct($user) 
    {
        $this->user = $user;
        $this->auth = new UserAuth($user);
    }

    public function changeSettings($settings)
    {
        if ($this->auth->verifyCredentials()) {
            // ...
        }
    }
}
```

**[#voltar para o topo](#sumário)**

### Princípio do Aberto/Fechado (OCP)

Conforme afirma Bertrand Meyer, "entidades de software (classes, módulos, funções,
etc.) deve estar aberto para extensão, mas fechado para modificação." O que isso
significa? Esse princípio basicamente afirma que você deve permitir que os usuários
adicione novas funcionalidades sem alterar o código existente.

**Ruim:**

```php
abstract class Adapter
{
    protected $name;

    public function getName()
    {
        return $this->name;
    }
}

class AjaxAdapter extends Adapter
{
    public function __construct()
    {
        parent::__construct();

        $this->name = 'ajaxAdapter';
    }
}

class NodeAdapter extends Adapter
{
    public function __construct()
    {
        parent::__construct();

        $this->name = 'nodeAdapter';
    }
}

class HttpRequester
{
    private $adapter;

    public function __construct($adapter)
    {
        $this->adapter = $adapter;
    }

    public function fetch($url)
    {
        $adapterName = $this->adapter->getName();

        if ($adapterName === 'ajaxAdapter') {
            return $this->makeAjaxCall($url);
        } elseif ($adapterName === 'httpNodeAdapter') {
            return $this->makeHttpCall($url);
        }
    }

    private function makeAjaxCall($url)
    {
        // request and return promise
    }

    private function makeHttpCall($url)
    {
        // request and return promise
    }
}
```

**Bom:**

```php
interface Adapter
{
    public function request($url);
}

class AjaxAdapter implements Adapter
{
    public function request($url)
    {
        // request and return promise
    }
}

class NodeAdapter implements Adapter
{
    public function request($url)
    {
        // request and return promise
    }
}

class HttpRequester
{
    private $adapter;

    public function __construct(Adapter $adapter)
    {
        $this->adapter = $adapter;
    }

    public function fetch($url)
    {
        return $this->adapter->request($url);
    }
}
```

**[#voltar para o topo](#sumário)**

### Princício da Substituição de Liskov (LSP)

Este é um termo assustador para um conceito muito simples. É formalmente definido como "Se S é um subtipo de T, então objetos do tipo T podem ser substituídos por objetos do tipo S (ou seja, objetos do tipo S podem substituir objetos do tipo T) sem alterar nenhuma das propriedades desejáveis desse programa. (correção, tarefa executada etc.) ". Essa é uma definição ainda mais assustadora.

A melhor explicação para isso é se você tiver uma classe pai e uma classe filho, então a classe base e a classe filho poderão ser usadas de forma intercambiável sem obter resultados incorretos. Isso ainda pode ser confuso, então vamos dar uma olhada no exemplo clássico do retângulo quadrado. Matematicamente, um quadrado é um retângulo, mas se você o modelar usando o relacionamento "is-a" por herança, você rapidamente terá problemas.

**Ruim:**

```php
class Rectangle
{
    protected $width = 0;
    protected $height = 0;

    public function render($area)
    {
        // ...
    }

    public function setWidth($width)
    {
        $this->width = $width;
    }

    public function setHeight($height)
    {
        $this->height = $height;
    }

    public function getArea()
    {
        return $this->width * $this->height;
    }
}

class Square extends Rectangle
{
    public function setWidth($width)
    {
        $this->width = $this->height = $width;
    }

    public function setHeight(height)
    {
        $this->width = $this->height = $height;
    }
}

function renderLargeRectangles($rectangles)
{
    foreach ($rectangles as $rectangle) {
        $rectangle->setWidth(4);
        $rectangle->setHeight(5);
        $area = $rectangle->getArea(); // BAD: Will return 25 for Square. Should be 20.
        $rectangle->render($area);
    }
}

$rectangles = [new Rectangle(), new Rectangle(), new Square()];
renderLargeRectangles($rectangles);
```

**Bom:**

```php
abstract class Shape
{
    protected $width = 0;
    protected $height = 0;

    abstract public function getArea();

    public function render($area)
    {
        // ...
    }
}

class Rectangle extends Shape
{
    public function setWidth($width)
    {
        $this->width = $width;
    }

    public function setHeight($height)
    {
        $this->height = $height;
    }

    public function getArea()
    {
        return $this->width * $this->height;
    }
}

class Square extends Shape
{
    private $length = 0;

    public function setLength($length)
    {
        $this->length = $length;
    }

    public function getArea()
    {
        return pow($this->length, 2);
    }
}

function renderLargeRectangles($rectangles)
{
    foreach ($rectangles as $rectangle) {
        if ($rectangle instanceof Square) {
            $rectangle->setLength(5);
        } elseif ($rectangle instanceof Rectangle) {
            $rectangle->setWidth(4);
            $rectangle->setHeight(5);
        }

        $area = $rectangle->getArea(); 
        $rectangle->render($area);
    }
}

$shapes = [new Rectangle(), new Rectangle(), new Square()];
renderLargeRectangles($shapes);
```

**[#voltar para o topo](#sumário)**

### Princípio da Segregação de interface (ISP)

O provedor declara que "os clientes não devem ser forçados a depender das interfaces que não usam".

Um bom exemplo que demonstra esse princípio é para
classes que requerem objetos de configurações grandes. Não é necessário exigir que os clientes configurem grandes quantidades de opções, pois na maioria das vezes eles não precisam de todas as configurações. Torná-los opcionais ajuda a evitar uma "interface gorda".

**Ruim:**

```php
interface Employee
{
    public function work();

    public function eat();
}

class Human implements Employee
{
    public function work()
    {
        // ....working
    }

    public function eat()
    {
        // ...... eating in lunch break
    }
}

class Robot implements Employee
{
    public function work()
    {
        //.... working much more
    }

    public function eat()
    {
        //.... robot can't eat, but it must implement this method
    }
}
```

**Bom:**

Nem todo trabalhador é um funcionário, mas todo funcionário é um trabalhador.

```php
interface Workable
{
    public function work();
}

interface Feedable
{
    public function eat();
}

interface Employee extends Feedable, Workable
{
}

class Human implements Employee
{
    public function work()
    {
        // ....working
    }

    public function eat()
    {
        //.... eating in lunch break
    }
}

// robot can only work
class Robot implements Workable
{
    public function work()
    {
        // ....working
    }
}
```

**[#voltar para o topo](#sumário)**

### Princípio da Injeção de dependências (DIP)

Este princípio afirma duas coisas essenciais:
1. Os módulos de alto nível não devem depender dos módulos de baixo nível. Ambos devem depender de abstrações.
2. As abstrações não devem depender de detalhes. Os detalhes devem depender das abstrações.

Ele pode ser difícil de entender no começo, mas se você já trabalhou com frameworks PHP (como o Symfony), já deve ter visto uma implementação deste princípio na forma de Injeção de Dependência ou Dependency Injection (DI). 
Embora não sejam conceitos idênticos, o DIP mantém o conhecimento dos módulos de alto nível sobre os seus módulos de baixo nível e configurá-los.
Isso pode ser feito através do DIP. Um dos grandes benefícios disso é que reduz o acoplamento entre os módulos. O acoplamento é um padrão de desenvolvimento muito ruim, porque dificulta a refatoração do seu código.

**Ruim:**

```php
class Employee
{
    public function work()
    {
        // ....working
    }
}

class Robot extends Employee
{
    public function work()
    {
        //.... working much more
    }
}

class Manager
{
    private $employee;

    public function __construct(Employee $employee)
    {
        $this->employee = $employee;
    }

    public function manage()
    {
        $this->employee->work();
    }
}
```

**Bom:**

```php
interface Employee
{
    public function work();
}

class Human implements Employee
{
    public function work()
    {
        // ....working
    }
}

class Robot implements Employee
{
    public function work()
    {
        //.... working much more
    }
}

class Manager
{
    private $employee;

    public function __construct(Employee $employee)
    {
        $this->employee = $employee;
    }

    public function manage()
    {
        $this->employee->work();
    }
}
```

**[#voltar para o topo](#sumário)**

### Use method chaining

Este padrão é muito útil e comumente usado em muitas bibliotecas, como como PHPUnit e Doctrine. Ele permite que seu código seja expressivo e menos verboso.
Por esse motivo, use o encadeamento de métodos (chaining method) e observe o quão limpo o seu código estará. Em seus métodos de classe, simplesmente use `return $this` no final de cada função `set`,
e você pode encadear outros métodos de classe nele.

**Ruim:**

```php
class Car 
{
    private $make = 'Honda';
    private $model = 'Accord';
    private $color = 'white';

    public function setMake($make)
    {
        $this->make = $make;
    }

    public function setModel($model)
    {
        $this->model = $model;
    }

    public function setColor($color)
    {
        $this->color = $color;
    }

    public function dump()
    {
        var_dump($this->make, $this->model, $this->color);
    }
}

$car = new Car();
$car->setColor('pink');
$car->setMake('Ford');
$car->setModel('F-150');
$car->dump();
```

**Bom:**

```php
class Car 
{
    private $make = 'Honda';
    private $model = 'Accord';
    private $color = 'white';

    public function setMake($make)
    {
        $this->make = $make;
        
        // NOTE: Returning this for chaining
        return $this;
    }

    public function setModel($model)
    {
        $this->model = $model;

        // NOTE: Returning this for chaining
        return $this;
    }

    public function setColor($color)
    {
        $this->color = $color;

        // NOTE: Returning this for chaining
        return $this;
    }

    public function dump()
    {
        var_dump($this->make, $this->model, $this->color);
    }
}

$car = (new Car())
  ->setColor('pink')
  ->setMake('Ford')
  ->setModel('F-150')
  ->dump();
```

**[#voltar para o topo](#sumário)**

### Prefira composição do que herança

Conforme declarado em [*Design Patterns*](https://en.wikipedia.org/wiki/Design_Patterns) pelo Gang of Four, você deve preferir composição do que herança onde puder. Há muitas boas razões para usar herança e muitas boas razões para usar composição.
O ponto principal desta máxima é que se sua mente instintivamente buscar herança, tente pensar se a composição poderia modelar melhor o seu problema. Em alguns casos pode.

Você pode estar se perguntando então, "quando devo usar herança?" Isto depende do seu problema em questão, mas esta é uma lista decente de quando a herança
faz mais sentido do que composição:

1. Sua herança representa um relacionamento "é um" e não um "tem um" relacionamento (Human -> Animal vs. User -> UserDetails).
2. Você pode reutilizar o código das classes base (os humanos podem se mover como todos os animais).
3. Você deseja fazer alterações globais nas classes derivadas alterando uma classe base. (Mude o gasto calórico de todos os animais quando eles se movem).

**Ruim:**

```php
class Employee 
{
    private $name;
    private $email;

    public function __construct($name, $email)
    {
        $this->name = $name;
        $this->email = $email;
    }

    // ...
}

// Bad because Employees "have" tax data. 
// EmployeeTaxData is not a type of Employee

class EmployeeTaxData extends Employee 
{
    private $ssn;
    private $salary;
    
    public function __construct($name, $email, $ssn, $salary)
    {
        parent::__construct($name, $email);

        $this->ssn = $ssn;
        $this->salary = $salary;
    }

    // ...
}
```

**Bom:**

```php
class EmployeeTaxData 
{
    private $ssn;
    private $salary;

    public function __construct($ssn, $salary)
    {
        $this->ssn = $ssn;
        $this->salary = $salary;
    }

    // ...
}

class Employee 
{
    private $name;
    private $email;
    private $taxData;

    public function __construct($name, $email)
    {
        $this->name = $name;
        $this->email = $email;
    }

    public function setTaxData($ssn, $salary)
    {
        $this->taxData = new EmployeeTaxData($ssn, $salary);
    }

    // ...
}
```

**[#voltar para o topo](#sumário)**

## Não repita você mesmo (DRY)

Tente observar o princípio [DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself) (Don't repeat yourself).

Faça o seu melhor absoluto para evitar códigos duplicados. O código duplicado é ruim porque significa que há mais de um lugar para alterar algo se você precisar mudar alguma lógica.

Imagine que você administra um restaurante e mantém o controle de seu inventário: todos os seus tomates, cebolas, alho, especiarias, etc. Se você tiver várias listas que você mantém isso, então tudo tem que ser atualizado quando você serve um prato com tomates neles. Se você tem apenas uma lista, só há um lugar para atualizar!

Frequentemente, você tem código duplicado porque tem duas ou mais coisas ligeiramente diferentes, que compartilham muito em comum, mas suas diferenças o forçam a ter duas ou mais funções separadas que fazem muitas das mesmas coisas. Remover código duplicado significa criar uma abstração que pode lidar com esse conjunto de coisas diferentes com apenas uma função / módulo / classe.

Obter a abstração certa é fundamental, por isso você deve seguir os princípios SOLID definidos na seção [Classes](#classes). Abstrações ruins podem ser piores do que código duplicado, então tome cuidado! Dito isso, se você pode fazer uma boa abstração, faça! Não se repita, caso contrário, você atualizará vários lugares sempre que quiser mudar alguma coisa.

**Ruim:**

```php
function showDeveloperList($developers)
{
    foreach ($developers as $developer) {
        $expectedSalary = $developer->calculateExpectedSalary();
        $experience = $developer->getExperience();
        $githubLink = $developer->getGithubLink();
        $data = [
            $expectedSalary,
            $experience,
            $githubLink
        ];

        render($data);
    }
}

function showManagerList($managers)
{
    foreach ($managers as $manager) {
        $expectedSalary = $manager->calculateExpectedSalary();
        $experience = $manager->getExperience();
        $githubLink = $manager->getGithubLink();
        $data = [
            $expectedSalary,
            $experience,
            $githubLink
        ];

        render($data);
    }
}
```

**Bom:**

```php
function showList($employees)
{
    foreach ($employees as $employee) {
        $expectedSalary = $employee->calculateExpectedSalary();
        $experience = $employee->getExperience();
        $githubLink = $employee->getGithubLink();
        $data = [
            $expectedSalary,
            $experience,
            $githubLink
        ];

        render($data);
    }
}
```

**Muito bom:**

É melhor usar uma versão compacta do código.

```php
function showList($employees)
{
    foreach ($employees as $employee) {
        render([
            $employee->calculateExpectedSalary(),
            $employee->getExperience(),
            $employee->getGithubLink()
        ]);
    }
}
```

**[#voltar para o topo](#sumário)**

## Traduções

Também disponível em outros idiomas:

* :cn: **Chinese:**
   * [php-cpm/clean-code-php](https://github.com/php-cpm/clean-code-php)
* :ru: **Russian:**
   * [peter-gribanov/clean-code-php](https://github.com/peter-gribanov/clean-code-php)
* :es: **Spanish:**
   * [fikoborquez/clean-code-php](https://github.com/fikoborquez/clean-code-php)
* :brazil: **Portuguese:**
   * [lucenarenato/clean-code-php](https://github.com/lucenarenato/clean-code-php)
   * [fabioars/clean-code-php](https://github.com/fabioars/clean-code-php)
   * [jeanjar/clean-code-php](https://github.com/jeanjar/clean-code-php/tree/pt-br)
* :thailand: **Thai:**
   * [panuwizzle/clean-code-php](https://github.com/panuwizzle/clean-code-php)
* :fr: **French:**
   * [errorname/clean-code-php](https://github.com/errorname/clean-code-php)
* :vietnam: **Vietnamese**
   * [viethuongdev/clean-code-php](https://github.com/viethuongdev/clean-code-php)
* :kr: **Korean:**
   * [yujineeee/clean-code-php](https://github.com/yujineeee/clean-code-php)
* :tr: **Turkish:**
   * [anilozmen/clean-code-php](https://github.com/anilozmen/clean-code-php)


**[#voltar para o topo](#sumário)**
