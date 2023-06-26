Домашнее задание по теме «NoSQL & MongoDB»:
Взять: https://onecompiler.com/mongodb/3zcr59ed9

Создать базу данных.

Вставить 4 документа по товарам на сайте. Атрибуты:
* название;
* категория — 2 товара из одной категории и 2 товара из другой;
* цена;
* количество товаров на складе.

Рассчитать остаточную стоимость товаров в каждой категории (сумма цены, умноженной на остаток).

Уменьшить количество товара на 1.

Вывести 2 самых дорогих товара.

Код:

db.employees.insertMany([

  {empId: 1, name: 'Milk', category: 'MP', cost: 70, quantity: 160 },
  
  {empId: 2, name: 'Cheese', category: 'MP', cost: 720, quantity: 10 },
  
  {empId: 3, name: 'Noodles', category: 'Grocery', cost: 55, quantity: 600 },
  
  {empId: 4, name: 'Olive oil', category: 'Grocery', cost: 450, quantity: 100 }
  
]);


db.employees.aggregate([
  
  { $group: 
  { _id: '$category', sum: { $sum: '$cost' }, 
  total_sum: { $sum: {$multiply: ['$cost', '$quantity'] } }  
  }}

])

db.employees.updateOne({empId:1},{$inc:{quantity:-1}})


db.employees.find().sort({"cost": -1 }).limit( 2 )
