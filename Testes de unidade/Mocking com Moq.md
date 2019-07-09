# Substituindo as dependências dos objetos com Moq

## Por que eu preciso de um dublê?
Quando desenvolvemos testes de unidade, é comum termos que trabalhar com objetos complexos, que contenham dependências, ou que se comportam como se estivessem em produção, como, por exemplo, uma consulta em um banco de dados ou uma integração com APIs. 
Esses comportamentos, porém, deixam nossos testes complexos, dependentes e lentos, tornando, assim, manter e rodar a suíte de testes inviável. Para resolver esses problemas usamos dublês, que são objetos que apenas substituem os objetos de produção simulando seu comportamento. 

Ou seja, quando queremos testar o comportamento de uma classe que contenha dependencias e queremos apenas simular um suposto comportamento de uma dependencia, então, usmaos dublês. 
Essa prtática permite a simulação da dependencia, retornando uma resposta esperada, sem chance de falhas causadas pelo ambiente de produção, ou de falha da resposta, sem que eu tenha que alterar nenhuma linha do código de produção para simular estes casos.

Existem vários tipos de dublês:

- Fakes:  
    Fakes são objetos que escrevemos com retornos fixo. São os mais trabalhosos de implementar e menos reutilizaveis, por isso são pouco utilizados na prática.  

- Stubs:  
    Stubs são objetos com dados pré definidos, prontos para serem retornados. Ideal para interações com bancos de dados.  

- Mocks:  
    Mocks são objetos moldados, eles nos oferecem um ferramental para moulda-los e analisarmos como eles se comportam.

Fakes e stubs são exemplos mais academicos, e é pela facilidade do uso e pelo ferramental mais elaborado, que vamos focar em estudar os mocks e, no nosso caso, a ferramenta Moq.

## Entendendo os Mocks

Mocks são objetos que envolvem uma interface, criando configurações para o comportamento da mesma. 
É possivel, com mocks, configurar o que um método de uma interface irá retornar, ou, se dado um parametro X, este metodo deve ou não lançar uma exceção. 
Podemos. também, verificar se o método foi chamado ou até quantas vezes o método foi chamado.

O Mock é responsável por receber e retornar configurações do comportamento de um objeto interno, criado automaticamente e já implementando a interface que passamos por parametro (de tipo genérico). Assim, se eu configurar um método da interface para responder sempre uma resposta X, quando o metodo a ser testado chamar este metodo, a resposta será X.

## O Moq

O Moq é uma biblioteca que nos permite utilizar os Mocks. Para instalar o pacote do Moq no seu projeto de testes .NET core basta executar o seguinte comando no diretório do projeto:

    dotnet add package Moq

Para instanciar um novo mock utilizando Moq, basta chamar o construtor da classe Mock, passando por parametro (de tipo genérico) a interface que o mock deve simular.

    var fooMock = new Mock<IFoo>();

É importante lembrar que o Mock em si não implementa a interface passada por parametro. Em sua estrutura, o mock possui uma propriedade publica chamada de Object, que é usada como output do mock, e essa sim implementando a interface. Então quando formos utilizar o mock, o código fica assim:  

    // sendo "bar" o objeto que iremos testar
    var bar = new Bar(fooMock.Object);

## Configurando o comportamento da dependência:

### Configurando um método
Podemos substituir o retorno de um método da interface.
Por exemplo, para confugurar o método GetById() de um repositório para sempre retornar um resultado esperado o códigpo ficaria assim:

    var id = 16;
    var expectedResult = new Result(){
        id = id
    }
    var repositoryMock = new Mock<IRepository>();
    repositoryMock.Setup(p=> p.GetById(id)).Returns(expectedResult);

Repare que para o resultado esperado ser retornado, o parametro passado para o método deve ser o numero 16.
Para que qualer numero pass a ser aceito para o parâmetro, precisamos passa por parametro a expressão:

    repositoryMock.Setup(p=> p.GetById(It.IsAny<int>())).Returns(expectedResult);

Assim, qualquer inteiro passado por parâmetro retornaria o resultado esperado.

### Configurando uma propriedade:

Se por alguma necessidade especifica você precise que sua interface contenha alguma propriedade, é possivel configurar esses comportamentos também. Para isso basta usar o método SetupPorperty()

    fooMock.SetupProperty(p=> p.Name, "teste");    

Assim, sempre que esta propriedade for chamada, ela conterá um valor esperado.

## Os Métodos de Verificação

Com o Moq, podemos verificar se um método da interface foi chamado com determinado parametro.

    fooMock.Verify(p=> p.doSomething(2));

Essa verificação funciona como um assert (verificação), ou seja, se o método não foi chamado, então o teste irá falhar.


## Referências

1. Test Doubles — Fakes, Mocks and Stubs - Michal Lipski  
https://blog.pragmatists.com/test-doubles-fakes-mocks-and-stubs-1a7491dfa3da - Acessado em 10/06/2019

2. Testes Unitários 101: Mocks, Stubs, Spies e todas essas palavras difíceis - Lucas Santos  
https://medium.com/trainingcenter/testes-unit%C3%A1rios-mocks-stubs-spies-e-todas-essas-palavras-dif%C3%ADceis-f2765ac87cc8 - Acessado em 10/06/2019

3. Video: Unit Testing: MOQ Framework - Microsoft Visual Studio: Robert Green e Phil Japikse  
   https://www.youtube.com/watch?v=dZ2Psa_Bn2Q - Acessado em 05/07/2019  

---
Autor: Henrique Felipe Urruth  
Data: 04/06/2019