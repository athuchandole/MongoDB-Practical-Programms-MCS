### MongoDB Tourism Database Example

In this example, we manage a **tourism** database, which includes information about tourism packages, tours, destinations, and customers. The database contains two collections: **turisum** (for tourism service providers) and **tour** (for the tours themselves).

### 1. **Setting Up the Database and Collections**

#### 1.1 **Create the `turisum` Database**
```javascript
use turisum
```

#### 1.2 **Inserting Data into the `turisum` Collection**
The `turisum` collection contains details about tourism service providers, their packages, and the associated rates.

```javascript
db.turisum.insert({
  name: "veenaword",
  rate: 9,
  package: [
    { pname: "shillong", cost: 10000 },
    { pname: "gujart", cost: 7000 },
    { pname: "karnataka", cost: 6000 }
  ]
})

db.turisum.insert({
  name: "rohit",
  rate: 7,
  package: [
    { pname: "shillong", cost: 10000 },
    { pname: "rujan", cost: 7000 }
  ]
})
```

#### 1.3 **Inserting Data into the `tour` Collection**
The `tour` collection stores details about tours, including source and destination, tourism service provider, rate, expenses, year, and customers.

```javascript
db.tour.insert({
  sourc: "john",
  destination: "shillong",
  toerisumName: "veenaword",
  tourisumrate: 8000,
  expense: 20000,
  year: 2018,
  customer: [
    { cname: "mukesh", city: "pune" },
    { cname: "abhijeetsangita", city: "baramati" },
    { cname: "manisha", city: "15no" },
    { cname: "manasi", city: "latur" }
  ]
})

db.tour.insert({
  sourc: "john",
  destination: "karnataka",
  toerisumName: "veenaword",
  tourisumrate: 80090,
  expense: 20900,
  year: 2017,
  customer: [
    { cname: "mukesh", city: "pune" },
    { cname: "abhijeetsangita", city: "baramati" },
    { cname: "manisha", city: "15no" },
    { cname: "manasi", city: "latur" }
  ]
})

db.tour.insert({
  sourc: "john",
  destination: "rajasthan",
  toerisumName: "rohit",
  tourisumrate: 6000,
  expense: 30400,
  year: 2019,
  customer: [
    { cname: "mukesh", city: "pune" },
    { cname: "abhijeetsangita", city: "baramati" },
    { cname: "manisha", city: "15no" },
    { cname: "manasi", city: "latur" }
  ]
})

db.tour.insert({
  sourc: "john",
  destination: "taj",
  toerisumName: "rohit",
  tourisumrate: 60090,
  expense: 10400,
  year: 2016,
  customer: [
    { cname: "mukesh", city: "pune" },
    { cname: "abhijeetsangita", city: "baramati" },
    { cname: "manisha", city: "15no" },
    { cname: "manasi", city: "latur" }
  ]
})
```

---

### 2. **Query Operations**

#### 2.1 **Find Tourism Providers Named "veenaword"**
This query retrieves information about the tourism provider "veenaword".

```javascript
db.turisum.find({ name: "veenaword" }).pretty()
```

#### 2.2 **Find the Tourism Provider with the Highest Rate**
This query sorts the tourism providers by rate in descending order and limits the result to the first one (the highest rated provider).

```javascript
db.turisum.find({}).sort({ "rate": -1 }).limit(1)
```

#### 2.3 **Calculate Total Expenses for the First 3 Tours Sorted by Year**
This query sorts tours by year in ascending order, limits the result to the first 3 tours, and then calculates the total expense of these tours.

```javascript
db.tour.aggregate([
  { "$sort": { "year": 1 } },
  { "$limit": 3 },
  { $group: { _id: null, "count": { "$sum": "$expense" } } }
])
```

#### 2.4 **Find Tours with Destination "shillong"**
This query retrieves all tours with the destination "shillong".

```javascript
db.tour.find({ destination: "shillong" })
```

---

### 3. **MongoDB Query Operators**

- **$sort**: Sorts the documents in ascending or descending order based on the specified field.
- **$limit**: Limits the number of documents returned by the query.
- **$group**: Aggregates documents into groups and performs aggregation operations (e.g., sum, average) on those groups.
- **$sum**: Sums the specified field within a group of documents.

---

### 4. **Sample Output**

#### 4.1 **Output of `db.turisum.find({ name: "veenaword" }).pretty()`**
```json
{
  "_id": ObjectId("..."),
  "name": "veenaword",
  "rate": 9,
  "package": [
    { "pname": "shillong", "cost": 10000 },
    { "pname": "gujart", "cost": 7000 },
    { "pname": "karnataka", "cost": 6000 }
  ]
}
```

#### 4.2 **Output of `db.turisum.find({}).sort({ "rate": -1 }).limit(1)`**
```json
{
  "_id": ObjectId("..."),
  "name": "veenaword",
  "rate": 9,
  "package": [
    { "pname": "shillong", "cost": 10000 },
    { "pname": "gujart", "cost": 7000 },
    { "pname": "karnataka", "cost": 6000 }
  ]
}
```

#### 4.3 **Output of `db.tour.aggregate([{"$sort": {"year": 1}}, {"$limit": 3}, {$group: {_id: null, "count": {"$sum": "$expense"}}}])`**
```json
[
  { "_id": null, "count": 81300 }
]
```

#### 4.4 **Output of `db.tour.find({ destination: "shillong" })`**
```json
[
  {
    "_id": ObjectId("..."),
    "sourc": "john",
    "destination": "shillong",
    "toerisumName": "veenaword",
    "tourisumrate": 8000,
    "expense": 20000,
    "year": 2018,
    "customer": [
      { "cname": "mukesh", "city": "pune" },
      { "cname": "abhijeetsangita", "city": "baramati" },
      { "cname": "manisha", "city": "15no" },
      { "cname": "manasi", "city": "latur" }
    ]
  }
]
```

---

### 5. **Conclusion**

This example demonstrates how to manage and query a MongoDB database for tourism-related information. The database includes details about tourism providers, tour destinations, expenses, and customer information. The queries show how to retrieve information based on specific criteria, such as finding the highest-rated tourism provider or calculating total expenses.
