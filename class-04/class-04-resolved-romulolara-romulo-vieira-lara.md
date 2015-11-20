# MongoDB - Aula 04 - Exercício
autor: ROMULO LARA

## **Adicionar** 2 ataques ao mesmo tempo para os seguintes pokemons: "Charmander", "Charmeleon" e "Ivysaur".
```
4dev(mongod-3.0.7) be-mean-pokemons> var query = {name: {$in: ["Charmander", "Charmeleon", "Ivysaur"]}}
4dev(mongod-3.0.7) be-mean-pokemons> var mod = {$pushAll: {type: ["attack1", "attack2"]}} 
4dev(mongod-3.0.7) be-mean-pokemons> var options = {multi: true}
4dev(mongod-3.0.7) be-mean-pokemons> db.pokemons.update(query, mod, options)
Updated 3 existing record(s) in 2ms
WriteResult({
  "nMatched": 3,
  "nUpserted": 0,
  "nModified": 3
})
4dev(mongod-3.0.7) be-mean-pokemons> db.pokemons.find(query)
{
  "_id": ObjectId("5645cd6a5611582d014617b7"),
  "name": "Charmander",
  "description": "Preferência por lugares quentes.",
  "type": [
    "fire",
    "attack1",
    "attack2"
  ],
  "attack": 52,
  "defence": 43,
  "height": 6
}
{
  "_id": ObjectId("5645cd6a5611582d014617b4"),
  "name": "Ivysaur",
  "description": "The bulb on its back grows as it absorbs nutrients. The bulb gives off a pleasant aroma when it blooms.",
  "type": [
    "grass",
    "attack1",
    "attack2"
  ],
  "attack": 62,
  "defence": 63,
  "height": 10
}
{
  "_id": ObjectId("5645cd6a5611582d014617b6"),
  "name": "Charmeleon",
  "description": "When it swings its burning tail, it elevates the temperature to unbearably high levels.",
  "type": [
    "fire",
    "attack1",
    "attack2"
  ],
  "attack": 64,
  "defence": 58,
  "height": 10
}
Fetched 3 record(s) in 2ms

```

## **Adicionar** 1 movimento em todos os pokemons: `desvio`.##
```
4dev(mongod-3.0.7) be-mean-pokemons> var query = {};
4dev(mongod-3.0.7) be-mean-pokemons> var mod = {$set: {moves: ["turning"]}}
4dev(mongod-3.0.7) be-mean-pokemons> var options = {multi: true}
4dev(mongod-3.0.7) be-mean-pokemons> db.pokemons.update(query, mod, options)
Updated 5 existing record(s) in 1ms
WriteResult({
  "nMatched": 5,
  "nUpserted": 0,
  "nModified": 5
})
4dev(mongod-3.0.7) be-mean-pokemons> db.pokemons.find()
{
  "_id": ObjectId("5645cd6a5611582d014617b7"),
  "name": "Charmander",
  "description": "Preferência por lugares quentes.",
  "type": [
    "fire",
    "attack1",
    "attack2"
  ],
  "attack": 52,
  "defence": 43,
  "height": 6,
  "moves": [
    "turning"
  ]
}
{
  "_id": ObjectId("5645cd6a5611582d014617b4"),
  "name": "Ivysaur",
  "description": "The bulb on its back grows as it absorbs nutrients. The bulb gives off a pleasant aroma when it blooms.",
  "type": [
    "grass",
    "attack1",
    "attack2"
  ],
  "attack": 62,
  "defence": 63,
  "height": 10,
  "moves": [
    "turning"
  ]
}
{
  "_id": ObjectId("5645cd6a5611582d014617b6"),
  "name": "Charmeleon",
  "description": "When it swings its burning tail, it elevates the temperature to unbearably high levels.",
  "type": [
    "fire",
    "attack1",
    "attack2"
  ],
  "attack": 64,
  "defence": 58,
  "height": 10,
  "moves": [
    "turning"
  ]
}
{
  "_id": ObjectId("5645cd6a5611582d014617b3"),
  "name": "Bulbasaur",
  "description": "The seed on its back is filled with nutrients. The seed grows steadily larger as its body grows.",
  "type": [
    "Poison"
  ],
  "attack": 49,
  "defence": 49,
  "height": 7,
  "moves": [
    "turning"
  ]
}
{
  "_id": ObjectId("5645cd6a5611582d014617b5"),
  "name": "Venusaur",
  "description": "It is able to con vert sunlight into energy. As a result, it is more powerful in the summertime.",
  "type": [
    "Poison"
  ],
  "attack": 82,
  "defence": 83,
  "height": 20,
  "moves": [
    "turning"
  ]
}
Fetched 5 record(s) in 2ms

```

## **Adicionar** o pokemon `NotFoundMon` caso ele não exista com todos os dados com o valor `null` e a descrição: "No information".##
```
4dev(mongod-3.0.7) be-mean-pokemons> var query = {name: "NotFoundMon"}
4dev(mongod-3.0.7) be-mean-pokemons> var options = {upsert: true}
4dev(mongod-3.0.7) be-mean-pokemons> var mod = {$set: {active: true}, $setOnInsert: {name: "NotFoundMon", description: "no information", type: [], attack: null, defence: null, height: null, moves: []} }
4dev(mongod-3.0.7) be-mean-pokemons> db.pokemons.update(query, mod, options)
Updated 1 new record(s) in 1ms
WriteResult({
  "nMatched": 0,
  "nUpserted": 1,
  "nModified": 0,
  "_id": ObjectId("564f518025cc475e20602f38")
})
4dev(mongod-3.0.7) be-mean-pokemons> db.pokemons.find({"_id": ObjectId("564f518025cc475e20602f38")})
{
  "_id": ObjectId("564f518025cc475e20602f38"),
  "name": "NotFoundMon",
  "active": true,
  "description": "no information",
  "type": [ ],
  "attack": null,
  "defence": null,
  "height": null,
  "moves": [ ]
}
Fetched 1 record(s) in 0ms

```

## Pesquisar todos os pokemons que possuam o tipo `fire` e mais um que você adicionou, escolha seu pokemon favorito.##
```
4dev(mongod-3.0.7) be-mean-pokemons> db.pokemons.find({type: {$in: ["grass", "fire"]}})
{
  "_id": ObjectId("5645cd6a5611582d014617b7"),
  "name": "Charmander",
  "description": "Preferência por lugares quentes.",
  "type": [
    "fire",
    "attack1",
    "attack2"
  ],
  "attack": 52,
  "defence": 43,
  "height": 6,
  "moves": [
    "turning"
  ]
}
{
  "_id": ObjectId("5645cd6a5611582d014617b4"),
  "name": "Ivysaur",
  "description": "The bulb on its back grows as it absorbs nutrients. The bulb gives off a pleasant aroma when it blooms.",
  "type": [
    "grass",
    "attack1",
    "attack2"
  ],
  "attack": 62,
  "defence": 63,
  "height": 10,
  "moves": [
    "turning"
  ]
}
{
  "_id": ObjectId("5645cd6a5611582d014617b6"),
  "name": "Charmeleon",
  "description": "When it swings its burning tail, it elevates the temperature to unbearably high levels.",
  "type": [
    "fire",
    "attack1",
    "attack2"
  ],
  "attack": 64,
  "defence": 58,
  "height": 10,
  "moves": [
    "turning"
  ]
}
Fetched 3 record(s) in 1ms
```

## Pesquisar **todos** os pokemons que possuam os ataques que você adicionou, escolha seu pokemon favorito.##
```
4dev(mongod-3.0.7) be-mean-pokemons> db.pokemons.find({type: {$all: ["attack1", "attack2"]}})
{
  "_id": ObjectId("5645cd6a5611582d014617b7"),
  "name": "Charmander",
  "description": "Preferência por lugares quentes.",
  "type": [
    "fire",
    "attack1",
    "attack2"
  ],
  "attack": 52,
  "defence": 43,
  "height": 6,
  "moves": [
    "turning"
  ]
}
{
  "_id": ObjectId("5645cd6a5611582d014617b4"),
  "name": "Ivysaur",
  "description": "The bulb on its back grows as it absorbs nutrients. The bulb gives off a pleasant aroma when it blooms.",
  "type": [
    "grass",
    "attack1",
    "attack2"
  ],
  "attack": 62,
  "defence": 63,
  "height": 10,
  "moves": [
    "turning"
  ]
}
{
  "_id": ObjectId("5645cd6a5611582d014617b6"),
  "name": "Charmeleon",
  "description": "When it swings its burning tail, it elevates the temperature to unbearably high levels.",
  "type": [
    "fire",
    "attack1",
    "attack2"
  ],
  "attack": 64,
  "defence": 58,
  "height": 10,
  "moves": [
    "turning"
  ]
}
Fetched 3 record(s) in 1ms
```

## Pesquisar **todos** os pokemons que não são do tipo `fire`.##
```
4dev(mongod-3.0.7) be-mean-pokemons> db.pokemons.find({type: {$ne: "fire"}})
{
  "_id": ObjectId("5645cd6a5611582d014617b4"),
  "name": "Ivysaur",
  "description": "The bulb on its back grows as it absorbs nutrients. The bulb gives off a pleasant aroma when it blooms.",
  "type": [
    "grass",
    "attack1",
    "attack2"
  ],
  "attack": 62,
  "defence": 63,
  "height": 10,
  "moves": [
    "turning"
  ]
}
{
  "_id": ObjectId("5645cd6a5611582d014617b3"),
  "name": "Bulbasaur",
  "description": "The seed on its back is filled with nutrients. The seed grows steadily larger as its body grows.",
  "type": [
    "Poison"
  ],
  "attack": 49,
  "defence": 49,
  "height": 7,
  "moves": [
    "turning"
  ]
}
{
  "_id": ObjectId("5645cd6a5611582d014617b5"),
  "name": "Venusaur",
  "description": "It is able to con vert sunlight into energy. As a result, it is more powerful in the summertime.",
  "type": [
    "Poison"
  ],
  "attack": 82,
  "defence": 83,
  "height": 20,
  "moves": [
    "turning"
  ]
}
{
  "_id": ObjectId("564f518025cc475e20602f38"),
  "name": "NotFoundMon",
  "active": true,
  "description": "no information",
  "type": [ ],
  "attack": null,
  "defence": null,
  "height": null,
  "moves": [ ]
}
Fetched 4 record(s) in 1ms
```

## Pesquisar **todos** os pokemons que tenham o ataque `fire` **E** tenham a defesa **não menor ou igual** a 49.##
```
4dev(mongod-3.0.7) be-mean-pokemons> db.pokemons.find({$and: [{type: {$eq: "fire"} }, {defence: {$not: {$lte: 49}} } ]})
{
  "_id": ObjectId("5645cd6a5611582d014617b6"),
  "name": "Charmeleon",
  "description": "When it swings its burning tail, it elevates the temperature to unbearably high levels.",
  "type": [
    "fire",
    "attack1",
    "attack2"
  ],
  "attack": 64,
  "defence": 58,
  "height": 10,
  "moves": [
    "turning"
  ]
}
Fetched 1 record(s) in 1ms
```

## Remova **todos** os pokemons do tipo `poison` e com attack menor que 50.
```
4dev(mongod-3.0.7) be-mean-pokemons> var query = {$and: [{type: {$in: [/poison/i]} }, {attack: {$lt: 50}} ]}
4dev(mongod-3.0.7) be-mean-pokemons> db.pokemons.find(query)
{
  "_id": ObjectId("5645cd6a5611582d014617b3"),
  "name": "Bulbasaur",
  "description": "The seed on its back is filled with nutrients. The seed grows steadily larger as its body grows.",
  "type": [
    "Poison"
  ],
  "attack": 49,
  "defence": 49,
  "height": 7,
  "moves": [
    "turning"
  ]
}
Fetched 1 record(s) in 1ms
4dev(mongod-3.0.7) be-mean-pokemons> db.pokemons.remove(query)
Removed 1 record(s) in 1ms
WriteResult({
  "nRemoved": 1
})
4dev(mongod-3.0.7) be-mean-pokemons> db.pokemons.find(query)
Fetched 0 record(s) in 1ms
```
