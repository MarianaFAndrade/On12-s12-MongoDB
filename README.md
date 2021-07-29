
# Banco de dados - Mongo DB
Criação de um banco de dados no Mongo DB com rotas de 
pesquisa, inclusão, alteração e exclusão de ítens.

A criação foi feita com um banco de dados criado para outro 
exercício da Reprograma que foi um Json de Livros.

#### Demandas de negócio
- Inserção de documentos
- Atualização de documentos
- Exclusão de documentos
- Consulta com projeção
- Consulta utilizando combinação entre os seletores
- Consulta paginada e ordenada (utilizar skip, limit e sort)


## Banco de dados - Rotas usadas para as demandas

#### Buscando Livros

```http
db.getCollection('livros').find({})
```
#### Inserindo um livro

```http
  db.livros.insertMany
```

#### Atualizando a quantidade de páginas do livro

```http
  db.getCollection('livros').update(
    {
        "nome" : "O Mistério da Estrela"
    },
    
    {
        $set:{'pagina': '269'}
    },
    
    {
        "multi" : false
    }
);
```

#### Excluindo um livro

```http
  db.getCollection('livros').remove({
    "categoria": { $ne: "AVENTURA" }
})
```

#### Consulta com projeção - Livros de Romance ordenados do maior para o menor número de páginas

```http
  db.getCollection('livros').find({categoria:'Romance'}).sort({pagina: 1})
```

#### Consulta combinando informações - Livros de Aventura com mais de 100 páginas

```http
  db.getCollection('livros').find({'categoria':'Aventura', 'pagina':{$gt:100}})
```

#### Consulta ordenada com (skip, limit e sort) - Livro de Aventura com a terceira menor quantidade de páginas

```http
db.getCollection('livros').find({'categoria':'Aventura'}).sort({pagina: 1}).skip(2).limit(1)
```