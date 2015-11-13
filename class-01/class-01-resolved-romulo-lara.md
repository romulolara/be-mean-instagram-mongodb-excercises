# MongoDB - Aula 01 - Exercício

autor: ROMULO LARA

## Importando os restaurantes

```
mongoimport --db be-mean --collection restaurantes --drop --file restaurantes.json 
2015-11-12T23:15:23.971-0200	connected to: localhost
2015-11-12T23:15:23.972-0200	dropping: be-mean.restaurantes
2015-11-12T23:15:26.948-0200	[##########..............] be-mean.restaurantes	5.2 MB/11.4 MB (45.5%)
2015-11-12T23:15:29.934-0200	[##########..............] be-mean.restaurantes	5.2 MB/11.4 MB (45.5%)
2015-11-12T23:15:32.934-0200	[##########..............] be-mean.restaurantes	5.2 MB/11.4 MB (45.5%)
2015-11-12T23:15:35.949-0200	[#############...........] be-mean.restaurantes	6.2 MB/11.4 MB (54.4%)
2015-11-12T23:15:38.953-0200	[####################....] be-mean.restaurantes	9.8 MB/11.4 MB (86.2%)
2015-11-12T23:15:40.335-0200	imported 25359 documents

```

## Contando os restaurantes

```
4dev(mongod-3.0.7) be-mean> db.restaurantes.find({}).count()
25359

```
