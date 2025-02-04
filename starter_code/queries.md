![Ironhack Logo](https://i.imgur.com/1QgrNNw.png)

# Answers

### 1. All the companies that it's name match 'Babelgum'. Retrieve only their `name` field.

F { name : "Babelgum" }
P { name: 1, _id:0 }

### 2. All the companies that have more than 5000 employees. Limit the search to 20 companies and sort them by **number of employees**.

F {number_of_employees: { $gt: 5000 }}
S {number_of_employees: 1}
L 20

### 3. All the companies founded between 2000 and 2005, both years included. Retrieve only the `name` and `founded_year` fileds.

F {founded_year: {$gte: 2000, $lte: 2005}}
P {founded_year: 1, name: 1, _id:0}

### 4. All the companies that had a Valuation Amount of more than 100.000.000 and have been founded before 2010. Retrieve only the `name` and `ipo` fields.

F {$and: [ {"acquisition.price_amount": {$gt: 100000000}}, {founded_year: {$lt: 2010}}] }
P {name:1,ipo:1,_id:0}

### 5. All the companies that have less than 1000 employees and have been founded before 2005. Order them by the number of employees and limit the search to 10 companies.

F {$and : [{number_of_employees: { $lt: 1000 }}, {founded_year: {$lt: 2005}}]}
S {number_of_employees:1}

### 6. All the companies that don't include the `partners` field.

F {partners: {$exists: false}}

### 7. All the companies that have a null type of value on the `category_code` field.

F {category_code: {$type: "null"}}

### 8. All the companies that have at least 100 employees but less than 1000. Retrieve only the `name` and `number of employees` fields.

F {number_of_employees: {$gte: 100, $lt: 1000}}
P {number_of_employees:1,name:1,_id:0}

### 9. Order all the companies by their IPO price descendently.

S {"ipo.valuation_amount":-1}

### 10. Retrieve the 10 companies with more employees, order by the `number of employees`

S {number_of_employees:-1}
L 10

### 11. All the companies founded on the second semester of the year. Limit your search to 1000 companies.

F {founded_month: {$gte: 6}}
L 1000

### 12. All the companies that have been 'deadpooled' after the third year.

F {$and: [{$and: [{deadpooled_year: {$ne: null}},{deadpooled_year: {$exists: true}}]}, {$or: [{deadpooled_year:{$gt: 3, $lt: 1000} },{ {$where: deadpooled_year>founded_year+3 }]}]} //No funciona

F  {$where: "deadpooled_year>founded_year+3"}  // Otra forma

### 13. All the companies founded before 2000 that have and acquisition amount of more than 10.000.000

F {$and: [{"acquisition.price_amount": {$gt: 10000000}},{founded_year: {$lt: 2000}}]}

### 14. All the companies that have been acquired after 2015, order by the acquisition amount, and retrieve only their `name` and `acquisiton` field.

$all

### 15. Order the companies by their `founded year`, retrieving only their `name` and `founded year`.

F {founded_year: {$ne: null}}
P {name:1, founded_year:1,_id:0}
S {founded_year:1}

### 16. All the companies that have been founded on the first seven days of the month, including the seventh. Sort them by their `aquisition price` descendently. Limit the search to 10 documents.

F {founded_day: {$lte: 7}}
S {"acquisition.price_amount":-1}
L 10

### 17. All the companies on the 'web' `category` that have more than 4000 employees. Sort them by the amount of employees in ascendant order.

F {$and: [{category_code: "web"},{number_of_employees: {$gt: 4000}}]}
S {number_of_employees: 1}

### 18. All the companies which their acquisition amount is more than 10.000.000, and currency are 'EUR'.

F {$and: [{"acquisition.price_amount": {$gt: 10000000}},{"acquisition.price_currency_code": "EUR"}]}

### 19. All the companies that have been acquired on the first trimester of the year. Limit the search to 10 companies, and retrieve only their `name` and `acquisition` fields.

F {"acquisition.acquired_month": {$lt: 4}}
P {name:1,_id:0,acquisition:1}
L 10

### 20. All the companies that have been founded between 2000 and 2010, but have not been acquired before 2011.

F {$and: [{founded_year: {$gt: 2000, $lt: 2010}},{"acquisition.acquired_year": {$gt: 2011}}]}