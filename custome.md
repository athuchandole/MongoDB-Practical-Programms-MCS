Here are the MongoDB queries for managing and querying **Mobile Shopping** data, including customer purchases and mobile details:

### 1. **Setting Up the Database and Collection**

#### 1.1 **Create the `custome` and `shopping` Collections**

```javascript
use custome
```

#### 1.2 **Inserting Data into the `custome` Collection**

The `custome` collection contains customer purchase information, including the customer name (`cname`), the mobile model purchased (`modelname`), and the purchase amount (`amount`).

```javascript
db.custome.insert({ cname: "mukesh", modelname: "samsungj6", amount: 20000 })
db.custome.insert({ cname: "abhijeet", modelname: "samsungj6", amount: 20060 })
db.custome.insert({ cname: "manasi", modelname: "iphone7+", amount: 30060 })
db.custome.insert({ cname: "manisha", modelname: "iphone7+", amount: 30070 })
db.custome.insert({ cname: "dipak", modelname: "iphone7+", amount: 30800 })
```

#### 1.3 **Inserting Data into the `shopping` Collection**

The `shopping` collection contains mobile brand details and the specific models along with their RAM, ROM, and price rate.

```javascript
db.shopping.insert({
  brandname: "samsung",
  rate: 6,
  model: [
    { mname: "s40", ram: "3GB", rom: "32GB", rate: 4 },
    { mname: "j6", ram: "4GB", rom: "32GB", rate: 7 },
    { mname: "j7", ram: "6GB", rom: "64GB", rate: 6 }
  ]
})
db.shopping.insert({
  brandname: "vivo",
  rate: 8,
  model: [
    { mname: "Y55", ram: "3GB", rom: "32GB", rate: 6 },
    { mname: "Ys5", ram: "4GB", rom: "32GB", rate: 4 },
    { mname: "YYY", ram: "6GB", rom: "64GB", rate: 6 }
  ]
})
```

---

### 2. **Query Operations**

#### 2.1 **Find Models with Specific RAM and ROM**

This query retrieves all mobile models that have **3GB RAM** and **32GB ROM**.

```javascript
db.shopping.find({ "model.ram": "3GB", "model.rom": "32GB" })
```

#### 2.2 **Find Customers Who Purchased the Samsung J6 Model**

This query finds all customers who purchased the **Samsung J6** model.

```javascript
db.custome.find({ modelname: "samsung j6" })
```

#### 2.3 **Find the Brand with the Highest Rate**

This query sorts the **shopping** collection by **rate** in descending order and limits the result to the top one brand. Then, it groups by **brandname** to find the brand with the highest rate.

```javascript
db.shopping.aggregate([
  { "$sort": { "rate": -1 } },
  { "$limit": 1 },
  { $group: { _id: "$brandname" } }
])
```

#### 2.4 **Sort Customers by Name in Ascending Order**

This query retrieves all customers sorted by their name (**cname**) in ascending order.

```javascript
db.custome.find().sort({ "cname": 1 })
```

---

### 3. **Sample Outputs**

#### 3.1 **Output of `db.shopping.find({ "model.ram": "3GB", "model.rom": "32GB" })`**
```json
[
  {
    "_id": ObjectId("..."),
    "brandname": "samsung",
    "rate": 6,
    "model": [
      { "mname": "s40", "ram": "3GB", "rom": "32GB", "rate": 4 },
      { "mname": "j6", "ram": "4GB", "rom": "32GB", "rate": 7 },
      { "mname": "j7", "ram": "6GB", "rom": "64GB", "rate": 6 }
    ]
  },
  {
    "_id": ObjectId("..."),
    "brandname": "vivo",
    "rate": 8,
    "model": [
      { "mname": "Y55", "ram": "3GB", "rom": "32GB", "rate": 6 },
      { "mname": "Ys5", "ram": "4GB", "rom": "32GB", "rate": 4 },
      { "mname": "YYY", "ram": "6GB", "rom": "64GB", "rate": 6 }
    ]
  }
]
```

#### 3.2 **Output of `db.custome.find({ modelname: "samsung j6" })`**
```json
[
  {
    "_id": ObjectId("..."),
    "cname": "mukesh",
    "modelname": "samsungj6",
    "amount": 20000
  },
  {
    "_id": ObjectId("..."),
    "cname": "abhijeet",
    "modelname": "samsungj6",
    "amount": 20060
  }
]
```

#### 3.3 **Output of `db.shopping.aggregate([{"$sort":{"rate":-1}},{"$limit":1},{$group:{_id:"$brandname"}}])`**
```json
[
  {
    "_id": "vivo"
  }
]
```

#### 3.4 **Output of `db.custome.find().sort({"cname":1})`**
```json
[
  {
    "_id": ObjectId("..."),
    "cname": "abhijeet",
    "modelname": "samsungj6",
    "amount": 20060
  },
  {
    "_id": ObjectId("..."),
    "cname": "dipak",
    "modelname": "iphone7+",
    "amount": 30800
  },
  {
    "_id": ObjectId("..."),
    "cname": "manisha",
    "modelname": "iphone7+",
    "amount": 30070
  },
  {
    "_id": ObjectId("..."),
    "cname": "manasi",
    "modelname": "iphone7+",
    "amount": 30060
  },
  {
    "_id": ObjectId("..."),
    "cname": "mukesh",
    "modelname": "samsungj6",
    "amount": 20000
  }
]
```

---

### 4. **Explanation of Query Operators and Methods**

- **`$sort`**: Sorts the documents based on the specified field, in this case, sorting by `rate` in descending order.
- **`$group`**: Used for grouping documents by a certain key (e.g., `brandname`) and performing aggregate operations.
- **`$limit`**: Limits the number of documents returned in the query result.

---

These queries help in retrieving various details like the top mobile brand, customer purchase data, and sorting the data based on different attributes.
