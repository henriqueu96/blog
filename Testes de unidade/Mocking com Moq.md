# Mocking com Moq

## Por que eu preciso de um dublê?
Quando desenvolvemos testes de unidade, é comum termos que trabalhar com objetos que se comportam como se estivessem em produção, como uma consulta em um banco de dados ou uma integração com APIs, por exemplo. Esses comportamentos porém, deixam nossos testes complexos, dependentes e lentos, tornando o teste inviável. Para resolver esses problemas usamos dublês, objetos que apenas simulam e subistituem os objetos de produção. 

Existem vários tipos de dublês:

- Fakes:  
    Fakes são objetos que escrevemos com retornos fixo, são os mais trabalhosos de implementar, por isso são pouco utilizados na prática.
- Stubs:  
    Stubs são objetos com dados pré definidos, prontos para serem retornados. Ideal para interações com bancos de dados.
- Mocks:  
    Mocks são objetos moldados para se comportarem como os objetos de produção

## O Moq

#### Setup

#### Verify

## Referências

1. Test Doubles — Fakes, Mocks and Stubs - Michal Lipski  
https://blog.pragmatists.com/test-doubles-fakes-mocks-and-stubs-1a7491dfa3da - Acessado em 10/06/2019

2. Testes Unitários 101: Mocks, Stubs, Spies e todas essas palavras difíceis - Lucas Santos  
https://medium.com/trainingcenter/testes-unit%C3%A1rios-mocks-stubs-spies-e-todas-essas-palavras-dif%C3%ADceis-f2765ac87cc8 - Acessado em 10/06/2019

---
Autor: Henrique Felipe Urruth  
Data: 04/06/2019