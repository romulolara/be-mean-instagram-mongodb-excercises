# MongoDB - Aula 02 - Exercício
autor: ROMULO LARA

## Listagem das databases (passo 2)

```
4dev(mongod-3.0.7) test> use be-mean-pokemons
switched to db be-mean-pokemons
4dev(mongod-3.0.7) be-mean-pokemons> show databases
test    → 0.078GB
local   → 0.078GB
be-mean → 0.078GB
``` 

## Listagem das coleções (passo 3)

```
4dev(mongod-3.0.7) be-mean-pokemons> show collections
4dev(mongod-3.0.7) be-mean-pokemons>
```

## Cadastro dos pokemons (passo 4)

```
var pokemons = [
{"name": "Bulbasaur", "description": "The seed on its back is filled with nutrients. The seed grows steadily larger as its body grows.", "type": "Poison", "attack": 49, "defence": 49, "height": 7}, 
{"name": "Ivysaur", "description": "The bulb on its back grows as it absorbs nutrients. The bulb gives off a pleasant aroma when it blooms.", "type": "grass", "attack": 62, "defence": 63, "height": 10}, 
{"name": "Venusaur", "description": "It is able to con vert sunlight into energy. As a result, it is more powerful in the summertime.", "type": "poison",  "attack": 82, "defence": 83, "height": 20}, 
{"name": "Charmeleon", "description": "When it swings its burning tail, it elevates the temperature to unbearably high levels.", "type": "fire", "attack": 64, "defence": 58, "height": 10}, 
{"name": "Charmander", "description": "Obviously prefers hot places. When it rains, steam is said to spout from the tip of its tail.", "type": "fire", "attack": 52, "defence": 43, "height": 6 }
]

4dev(mongod-3.0.7) be-mean-pokemons> db.pokemons.insert(pokemons)
Inserted 1 record(s) in 7293ms
BulkWriteResult({
  "writeErrors": [ ],
  "writeConcernErrors": [ ],
  "nInserted": 5,
  "nUpserted": 0,
  "nMatched": 0,
  "nModified": 0,
  "nRemoved": 0,
  "upserted": [ ]
})

```

## Lista dos pokemons (passo 5)

```
4dev(mongod-3.0.7) be-mean-pokemons> db.pokemons.find()
{
  "_id": ObjectId("5645cd6a5611582d014617b3"),
  "name": "Bulbasaur",
  "description": "The seed on its back is filled with nutrients. The seed grows steadily larger as its body grows.",
  "type": "Poison",
  "attack": 49,
  "defence": 49,
  "height": 7
}
{
  "_id": ObjectId("5645cd6a5611582d014617b4"),
  "name": "Ivysaur",
  "description": "The bulb on its back grows as it absorbs nutrients. The bulb gives off a pleasant aroma when it blooms.",
  "type": "grass",
  "attack": 62,
  "defence": 63,
  "height": 10
}
{
  "_id": ObjectId("5645cd6a5611582d014617b5"),
  "name": "Venusaur",
  "description": "It is able to con vert sunlight into energy. As a result, it is more powerful in the summertime.",
  "type": "poison",
  "attack": 82,
  "defence": 83,
  "height": 20
}
{
  "_id": ObjectId("5645cd6a5611582d014617b6"),
  "name": "Charmeleon",
  "description": "When it swings its burning tail, it elevates the temperature to unbearably high levels.",
  "type": "fire",
  "attack": 64,
  "defence": 58,
  "height": 10
}
{
  "_id": ObjectId("5645cd6a5611582d014617b7"),
  "name": "Charmander",
  "description": "Obviously prefers hot places. When it rains, steam is said to spout from the tip of its tail.",
  "type": "fire",
  "attack": 52,
  "defence": 43,
  "height": 6
}
Fetched 5 record(s) in 1ms

```

## Charmander (passo 6)

```
4dev(mongod-3.0.7) be-mean-pokemons> var poke = db.pokemons.findOne({"name": "Charmander"})
4dev(mongod-3.0.7) be-mean-pokemons> poke
{
  "_id": ObjectId("5645cd6a5611582d014617b7"),
  "name": "Charmander",
  "description": "Obviously prefers hot places. When it rains, steam is said to spout from the tip of its tail.",
  "type": "fire",
  "attack": 52,
  "defence": 43,
  "height": 6
}
```

## Atualização do Charmander (passo 7)

```
4dev(mongod-3.0.7) be-mean-pokemons> var poke = db.pokemons.findOne({"name": "Charmander"})
4dev(mongod-3.0.7) be-mean-pokemons> poke
{
  "_id": ObjectId("5645cd6a5611582d014617b7"),
  "name": "Charmander",
  "description": "Obviously prefers hot places. When it rains, steam is said to spout from the tip of its tail.",
  "type": "fire",
  "attack": 52,
  "defence": 43,
  "height": 6
}
4dev(mongod-3.0.7) be-mean-pokemons> poke.description = "Preferência por lugares quentes."
Preferência por lugares quentes.
4dev(mongod-3.0.7) be-mean-pokemons> db.pokemons.save(poke)
Updated 1 existing record(s) in 1ms
WriteResult({
  "nMatched": 1,
  "nUpserted": 0,
  "nModified": 1
})
4dev(mongod-3.0.7) be-mean-pokemons> db.pokemons.findOne({"name": "Charmander"})
{
  "_id": ObjectId("5645cd6a5611582d014617b7"),
  "name": "Charmander",
  "description": "Preferência por lugares quentes.",
  "type": "fire",
  "attack": 52,
  "defence": 43,
  "height": 6
}

```
