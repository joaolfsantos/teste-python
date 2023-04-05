# Teste Técnico Desenvolvedor(a) Python

Neste repositório você encontra o enunciado do teste técnico.
Você provavelmente chegou aqui através da indicação de alguma pessoa da empresa após passar pelas **outras etapas**
do processo seletivo. Se este não for o seu caso e mesmo assim você implementar
alguma solução para este exercício ele **não** será avaliado.

> Você _pode_ usar o problema descrito aqui para exercitar suas habilidades de
> desenvolvimento, mas a sua solução será avaliada por alguém da Neocredit
> **apenas se** você estiver no processo seletivo.

## O problema

A equipe de desenvolvimento da Neocredit se orgulha de 
usar as tecnologias mais recentes e modernas. Essa regra também se aplica aos
projetos desenvolvidos em Python pela equipe.

Para garantir que todos seus projetos em Python estão usando as últimas versões
disponíves dos pacotes, a equipe pensou em criar uma ferramenta batizada de 
MagPy. A ferramenta recebe um nome de projeto, uma lista de pacotes e devolve a 
última versão de cada pacote.

Um dos integrantes apontou que a 
[API pública do PyPI](https://warehouse.readthedocs.io/api-reference/json.html)
poderia ser usada para esse fim.

## A Solução

Você deve desenvolver a MagPy, uma API REST que gerencia uma coleção de 
projetos. Cada projeto tem um nome e uma lista de pacotes. Cada pacote tem um 
nome e uma versão.

O cadastro de um projeto recebe o nome e a lista de pacotes. Cada pacote da 
lista precisa obrigatoriamente especificar um nome, mas a versão é opcional.

Sua API deve validar o projeto cadastrado: todos os pacotes informados devem
estar cadastrados no [PyPI](https://pypi.org/). Portanto você deve verificar o
nome e a versão do pacote.

Quando o pacote vem apenas com o nome, sua API deve assumir que é preciso usar
a última versão publicada no [PyPI](https://pypi.org/).

Abaixo, alguns exemplos de chamadas que serão feitas nessa API:

### Listagem de Projetos (LIST)
```
GET /api/projects
[
 {
    "name": "titan",
    "packages": [
        {"name": "graphene", "version": "1900"}
    ]
 },
 {
    "name": "godzilla",
    "packages": [
        {"name": "pandas", "version": "1.2"}
    ]
 }
]
```

### Cadastro de Projeto (CREATE)
```
POST /api/projects
{
    "name": "titan",
    "packages": [
        {"name": "Django"},
        {"name": "graphene", "version": "2.0"}
    ]
}
```
O código HTTP de retorno deve ser 201 e o corpo esperado na resposta é:
```
{
    "name": "titan",
    "packages": [
        {"name": "Django", "version": "3.2.5"},  // Usou a versão mais recente
        {"name": "graphene", "version": "2.0"}   // Manteve a versão especificada
    ]
}
```

Se um dos pacotes informados não existir, ou uma das versões especificadas for
inválida, um erro deve ser retornado, explicando o que houve.

Ex.: Para uma chamada semelhante ao exemplo abaixo:
```
POST /api/projects
{
    "name": "titan",
    "packages": [
        {"name": "pypypypypypypypypypypy"},
        {"name": "graphene", "version": "1900"}
    ]
}
```
O código HTTP de retorno deve ser 400 e o corpo esperado na resposta é:
```
{
    "error": "O pacote 'pypypypypypypypypypypy' não existe"
}
```

### Detalhes de um Projeto (RETRIEVE)
Também deve ser possível visitar projetos previamente cadastrados, usando o
nome na URL:
```
GET /api/projects/titan
{
    "name": "titan",
    "packages": [
        {"name": "Django", "version": "3.2.5"},
        {"name": "graphene", "version": "2.0"}
    ]
}
```

### Remoção de um Projeto (DELETE)
E deletar projetos pelo nome:
```
DELETE /api/projects/titan
```
O código HTTP de retorno deve ser 204, sem conteúdo.

<br/>

| ⚠️ | Sua solução deve usar a [API pública do PyPI](https://warehouse.readthedocs.io/api-reference/json.html). Não use outro caminho pra buscar as informações necessárias |
| --- | --- |


## Solução

Você pode usar seu framework web favorito desde que sua solução use Python (FastAPI, Flask, Django...). 
Se você nunca mexeu com nenhuma dessas opções, a recomendação é usar o FastAPI.

Para implementar sua solução, você precisará:

1. Fazer um **Fork** deste repositório.
2. Clonar o repositório criado na etapa anterior para sua máquina.
3. Criar uma nova branch e implementar a sua solução dentro dela.
3. Subir as alterações.
4. Abrir um PR **desta branch para a main** e enviar para o time da Neocredit o **link do PR** para que a sua solução seja avaliada.

**Boa sorte!**
