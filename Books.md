### MongoDB Example for Books and Publishers

In this example, we create two collections: **Books** and **Publishers**, and perform several MongoDB queries related to books, their authors, and the publishers.

### 1. **Setting up Collections and Data**

#### 1.1 **Create the `book` Database**
```javascript
use book
```

#### 1.2 **Inserting Data into the `book` Collection**
The `book` collection stores details about books, including their name, cost, author, and year of publication.

```javascript
db.book.insert({ BName: "shyamchiaai", cost: 500, author: "sane guruji", published: 2005 })
db.book.insert({ BName: "Two Saints", cost: 2000, author: "raguramkrishna", published: 2015 })
db.book.insert({ BName: "ramkrushnaparamhans", cost: 1000, author: "raguramkrishna", published: 2020 })
db.book.insert({ BName: "DMS", cost: 100, author: "raguramkrishna", published: 2007 })
```

#### 1.3 **Inserting Data into the `publisher` Collection**
The `publisher` collection stores details about the publishers, including their name, language, list of books, and city.

```javascript
db.publisher.insert({
  pname: "OReilly",
  language: "English",
  books: [{ BName: "ramkrushnaparamhans" }, { BName: "Two Saints" }],
  city: "mumbai"
})

db.publisher.insert({
  pname: "vision",
  language: "English",
  books: [{ BName: "DMS" }],
  city: "pune"
})

db.publisher.insert({
  pname: "OReilly",
  language: "marathi",
  books: [{ BName: "shyamchiaai" }],
  city: "mumbai"
})
```

---

### 2. **Query Operations**

#### 2.1 **Find Publishers in Mumbai**
This query finds all publishers located in the city of Mumbai:

```javascript
db.publisher.find({ city: "mumbai" })
```

#### 2.2 **Find Books with a Cost Less Than 1000**
This query retrieves all books whose cost is less than 1000:

```javascript
db.book.find({ cost: { $lt: 1000 } })
```

#### 2.3 **Find Books by "raguramkrishna" Published After 2017**
This query finds all books written by "raguramkrishna" and published after the year 2017:

```javascript
db.book.find({ author: "raguramkrishna", published: { $gt: 2017 } })
```

#### 2.4 **Find Publishers with Either English or Marathi Books (Using `$or`)**
This query finds publishers who either publish books in English or Marathi (using the `$or` operator):

```javascript
db.publisher.find({
  pname: "OReilly",
  $or: [{ language: "English" }, { language: "marathi" }]
})
```

---

### 3. **MongoDB Query Operators**

- **$lt (Less Than)**: Used to query for values less than a specified number. In this case, we use it to find books with a cost less than 1000.
- **$gt (Greater Than)**: Used to query for values greater than a specified number. In this case, it is used to find books published after 2017.
- **$or (Logical OR)**: Used to combine multiple conditions, where at least one condition needs to be true. In this case, it’s used to find publishers who publish books in either English or Marathi.

---

### 4. **Sample Output**

#### 4.1 **Output of `db.publisher.find({ city: "mumbai" })`**
```json
[
  { "_id": ObjectId("..."), "pname": "OReilly", "language": "English", "books": [{ "BName": "ramkrushnaparamhans" }, { "BName": "Two Saints" }], "city": "mumbai" },
  { "_id": ObjectId("..."), "pname": "OReilly", "language": "marathi", "books": [{ "BName": "shyamchiaai" }], "city": "mumbai" }
]
```

#### 4.2 **Output of `db.book.find({ cost: { $lt: 1000 } })`**
```json
[
  { "_id": ObjectId("..."), "BName": "shyamchiaai", "cost": 500, "author": "sane guruji", "published": 2005 },
  { "_id": ObjectId("..."), "BName": "DMS", "cost": 100, "author": "raguramkrishna", "published": 2007 },
  { "_id": ObjectId("..."), "BName": "ramkrushnaparamhans", "cost": 1000, "author": "raguramkrishna", "published": 2020 }
]
```

#### 4.3 **Output of `db.book.find({ author: "raguramkrishna", published: { $gt: 2017 } })`**
```json
[
  { "_id": ObjectId("..."), "BName": "ramkrushnaparamhans", "cost": 1000, "author": "raguramkrishna", "published": 2020 }
]
```

#### 4.4 **Output of `db.publisher.find({ pname: "OReilly", $or: [{ language: "English" }, { language: "marathi" }] })`**
```json
[
  { "_id": ObjectId("..."), "pname": "OReilly", "language": "English", "books": [{ "BName": "ramkrushnaparamhans" }, { "BName": "Two Saints" }], "city": "mumbai" },
  { "_id": ObjectId("..."), "pname": "OReilly", "language": "marathi", "books": [{ "BName": "shyamchiaai" }], "city": "mumbai" }
]
```

---

### 5. **Conclusion**

This example demonstrates how MongoDB can be used to manage books and publishers, with queries that filter based on various conditions such as cost, author, publication year, and language. The use of operators like `$lt`, `$gt`, and `$or` makes MongoDB's querying capabilities powerful and flexible.

---
