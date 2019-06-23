# Testes com NUnit 

## Por que escrever testes de unidade?

Ao desenvolver teste de unidade, nós, desenvolvedores, entendemos melhor a utilização da feature que estamos escrevendo, otimizando assim os parâmetros e retornos dessa feature, gerando código mais legível e confiável.

Ao modo em que vamos desenvolvendo novas features, vamos também sobrepondo e estendendo códigos de features anteriores, e é aí que os testes de unidade nos asseguram que essas mudanças não causaram impactos negativos no sistema, gerando, assim, segurança para o desenvolvedor e solidez para nosso código.

"Se está difícil escrever um teste automatizado, é porque provavelmente o código de produção está complicado"[1]. Essa afirmativa trás os testes de unidade como uma métrica de qualidade do design do código. Se uma feature é facilmente testável, significa que ela provavelmente foi bem escrita.

## Mas como funciona um teste de unidade?

Testes de unidade são pedaços de código desenvolvidos para executar uma funcionalidade específica, assegurando que um certo comportamento ocorra. Logo, ao testar o método de soma, por exemplo, podemos passar os parâmetros 2 e 1 assegurando que o resultado seja 3, se for, o teste resultara sucesso, se não for, o teste apontara a discrepância entre os valores.

Para manter esses pedaços de código, funcionais e legíveis, pode-se dividi-los em 3 partes distintas, chamamos essa técnica de "padrão 3A".

Preparar (ou arrange): Preparar a feature e as condições para que a mesma ela ocorra, como instanciar as dependências ou ajustar cenários. 
Agir (ou act): Chamar a feature, passando os parâmetros referentes ao comportamento que está sendo testado. 
Assegurar (ou assert): Fazer afirmações sobre como a feture deveria responder a ação, seja no seu retorno como em suas dependências.

## O NUnit

NUnit é um framework de teste de unidade compatível com qualquer linguagem .NET. 
No Principio, o NUnit foi portado do JUnit, porém, a partir da versão 3, foi completamente reescrito com novas funcionalidades e suporte para a maioria das plataformas .NET.

    using NUnit.Framework;
    using FooBarApp.Domain;

    namespace FooBarApp.Tests
    {
        [TestFixture]
        public class FooTests
        {
            [Test]
            public void DoSomethingElseShouldReturnExpectedValue()
            {
                // Arrange
                var foo = new Foo();

                // Act
                var actual = foo.DoSomethingElse("value");

                // Assert
                Assert.AreEqual("Expected value", actual);
            }
        }
    }

#### TestFixure
Toda classe que contém testes de unidade com NUnit possui a anotação TestFixure em sua declaração. Essa anotação serve para informar ao NUnit que esta classe contém testes e, opcionalmente, métodos de configuração e correção. Assim, quando iniciarmos o processo de teste, o NUnit busca nessas classes os testes.

#### Test
O atributo Test é uma maneira de definir um método como um teste dentro de uma classe TestFixture. Isso significa que o NUnit mapeará o método marcado e o adicionará a uma suíte de testes, analisando sua execução e verificações, gerando um resultado.

## Asserting (Assegurando)
Asserts são os métodos que determinam se o resultado de um teste é uma falha ou sucesso. Se um assert receber um parâmetro que não condiz com o comportamento esperado, então o teste é dado com uma falha. Por exemplo, se eu chamar o método Assert.Less(x,5), que assegura que o primeiro valor é menor que o segundo, e o valor de x for realmente menor que 5 então o teste ira passar, caso contrário o resultado do teste será uma falha.

Alguns exemplos de métodos contidos na classe Assert (NUnit.Framework.Assert):

- Equalidade:  
AreEqual() - Para garantir que um objeto tem o mesmo valor que outro 
- Identidade:  
AreSame() - Para garantir que um objeto tem a mesma referencia do que outro 
- Condições:  
IsTrue() - Para garantir que um valor é verdadeiro  
IsFalse() - Para garantir que um valor é falso  
Null() - Para garantir que um valor é nulo  
NotNull() - Para garantir que um valor não é nulo  
- Comparações:   
Less() - Para garantir que um valor é menor que outro  
Greater() - Para garantir que um valor é maior que outro 

## Como começar?

Para começar, vamos criar uma pasta onde ficara nosso projeto de testes e criar o projeto.

    $ mkdir HelloTests
    $ cd HelloTests
    $ dotnet new nunit 

Agora, podemos criar e editar nossos testes e rodar o comando para executar os testes.

    $ dotnet test 

A partir daí o dotnet executa os testes e informa o resultado.

    Build started, please wait...
    Build completed.

    Test run for HelloTests.dll(.NETCoreApp,Version=v2.1)
    Microsoft (R) Test Execution Command Line Tool Version 15.9.0
    Copyright (c) Microsoft Corporation.  All rights reserved.

    Starting test execution, please wait...

    Total tests: 1. Passed: 1. Failed: 0. Skipped: 0.
    Test Run Successful.
    Test execution time: 1.1288 Seconds

## Referências

1. Test-Driven Development - Maurício Aniche  
https://tdd.caelum.com.br/ - Acessado em 15/04/2019
2. Test-driven development as a defect-reduction practice - L. Williams ; E.M. Maximilien ; M. Vouk  
https://ieeexplore.ieee.org/abstract/document/1251029 - Acessado em 15/04/2019
3. Unit Testing with JUnit - vogella  
https://www.vogella.com/tutorials/JUnit/article.html - Acessado em 16/04/2019
4. 3A – Arrange, Act, Assert - Bill Wake  
https://xp123.com/articles/3a-arrange-act-assert - Acessado em 16/04/2019
5. Teste unitário e Qualidade de Software - Diogo Miranda  
https://medium.com/assertqualityassurance/teste-unit%C3%A1rio-e-qualidade-de-software-acce7b9c537 - Acessado em 16/04/2019
6. NUnit Documentation - NUnit org  
https://nunit.org - Acessado em 16/04/2019
 
---
Autor: Henrique Felipe Urruth  
Data: 04/06/2019