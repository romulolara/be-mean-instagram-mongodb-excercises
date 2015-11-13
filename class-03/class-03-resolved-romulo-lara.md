# MongoDB - Aula 03 - Exercício
autor: ROMULO LARA

## Liste todos Pokemons com a altura **menor que** 7;
```
4dev(mongod-3.0.7) be-mean-pokemons> db.pokemons.find({height: {$lt: 7}})
{
  "_id": ObjectId("5645cd6a5611582d014617b7"),
  "name": "Charmander",
  "description": "Preferência por lugares quentes.",
  "type": "fire",
  "attack": 52,
  "defence": 43,
  "height": 6
}
Fetched 1 record(s) in 1ms
```

## Liste todos Pokemons com a altura **maior ou igual que** 7
```
4dev(mongod-3.0.7) be-mean-pokemons> db.pokemons.find({height: {$gte: 7}})
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
Fetched 4 record(s) in 1ms
```

## Liste todos Pokemons com a altura **menor ou igual que** 7 **E** do tipo Poison
```
4dev(mongod-3.0.7) be-mean-pokemons> db.pokemons.find({$and : [{height: {$lte: 7}}, {type: "Poison"}]})
{
  "_id": ObjectId("5645cd6a5611582d014617b3"),
  "name": "Bulbasaur",
  "description": "The seed on its back is filled with nutrients. The seed grows steadily larger as its body grows.",
  "type": "Poison",
  "attack": 49,
  "defence": 49,
  "height": 7
}
Fetched 1 record(s) in 2ms
```

## Liste todos Pokemons com o name `Venusaur` **OU** com attack **menor ou igual que** 52
``` 
4dev(mongod-3.0.7) be-mean-pokemons> db.pokemons.find({$or : [{attack: {$lte: 52}}, {name: "Venusaur"}]})
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
  "_id": ObjectId("5645cd6a5611582d014617b5"),
  "name": "Venusaur",
  "description": "It is able to con vert sunlight into energy. As a result, it is more powerful in the summertime.",
  "type": "poison",
  "attack": 82,
  "defence": 83,
  "height": 20
}
{
  "_id": ObjectId("5645cd6a5611582d014617b7"),
  "name": "Charmander",
  "description": "Preferência por lugares quentes.",
  "type": "fire",
  "attack": 52,
  "defence": 43,
  "height": 6
}
Fetched 3 record(s) in 1ms
```

## Liste todos Pokemons com o attack **MAIOR OU IGUAL QUE** 48 **E** com  height **menor ou igual que** 7
```
4dev(mongod-3.0.7) be-mean-pokemons> db.pokemons.find({$and : [{attack: {$gte: 48}}, {height: {$lte: 7}}]})
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
  "_id": ObjectId("5645cd6a5611582d014617b7"),
  "name": "Charmander",
  "description": "Preferência por lugares quentes.",
  "type": "fire",
  "attack": 52,
  "defence": 43,
  "height": 6
}
Fetched 2 record(s) in 0ms
```

