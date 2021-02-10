Here are the queries you can use for managing and querying an **`item`** collection in MongoDB. The collection stores details about various items, including their name, status, dimensions, quantity in stock, and the quantity available at different warehouses.

### 1. **Setting Up the Database and Collection**

#### 1.1 **Create the `item` Database**
```javascript
use item
```

#### 1.2 **Inserting Data into the `item` Collection**
This step inserts data about various items (e.g., "planner," "toycar," "roboticcar," "bag"), including details such as the item name, tags, status, height, width, instock quantity, and the quantity available in each warehouse.

```javascript
db.item.insert({
  itemName: "planner",
  tag: ["wash", "food", "vehicle"],
  status: "A",
  height: 5,
  width: 9,
  instack: 15,
  warehouse: [
    { location: "pune", quntity: 36 },
    { location: "mumbai", quntity: 67 }
  ]
})

db.item.insert({
  itemName: "toycar",
  tag: ["food", "vehicle"],
  status: "D",
  height: 5,
  width: 9,
  instack: 15,
  warehouse: [
    { location: "pune", quntity: 36 },
    { location: "mumbai", quntity: 67 }
  ]
})

db.item.insert({
  itemName: "roboticcar",
  tag: ["food", "vehicle"],
  status: "A",
  height: 9,
  width: 9,
  instack: 5,
  warehouse: [
    { location: "pune", quntity: 26 },
    { location: "mumbai", quntity: 17 }
  ]
})

db.item.insert({
  itemName: "bag",
  tag: ["food", "vehicle", "school", "travel"],
  status: "C",
  height: 19,
  width: 39,
  instack: 75,
  warehouse: [
    { location: "surat", quntity: 26 },
    { location: "lanavala", quntity: 17 }
  ]
})
```

---

### 2. **Query Operations**

#### 2.1 **Find Items with Status 'D' and Warehouse Quantity Greater Than 30**
This query finds items with a status of **'D'** and where the warehouse quantity is greater than 30.

```javascript
db.item.find({ status: "D", "warehouse.quntity": { $gt: 30 } })
```

#### 2.2 **Find Items with Exactly 3 Tags**
This query finds items where the `tag` array contains exactly **3 tags**.

```javascript
db.item.find({ "tag": { $size: 3 } })
```

#### 2.3 **Find Items with Status 'A' or Warehouse Quantity Less Than 30 and Height Greater Than 10**
This query looks for items with a status of **'A'**, or items where the warehouse quantity is less than 30 and the height is greater than 10.

```javascript
db.item.find({ 
  $or: [
    { status: "A" },
    { "warehouse.quntity": { $lt: 30 }, height: { $gt: 10 } }
  ]
})
```

#### 2.4 **Find Items Named 'Planner' with Instock Quantity Less Than 20**
This query finds the **'planner'** item where the instock quantity is less than **20**.

```javascript
db.item.find({ itemName: "planner", instack: { $lt: 20 } })
```

---

### 3. **Sample Outputs**

#### 3.1 **Output of `db.item.find({ status: "D", "warehouse.quntity": { $gt: 30 } })`**
```json
[
  {
    "_id": ObjectId("..."),
    "itemName": "toycar",
    "tag": ["food", "vehicle"],
    "status": "D",
    "height": 5,
    "width": 9,
    "instack": 15,
    "warehouse": [
      { "location": "pune", "quntity": 36 },
      { "location": "mumbai", "quntity": 67 }
    ]
  }
]
```

#### 3.2 **Output of `db.item.find({ "tag": { $size: 3 } })`**
```json
[
  {
    "_id": ObjectId("..."),
    "itemName": "bag",
    "tag": ["food", "vehicle", "school", "travel"],
    "status": "C",
    "height": 19,
    "width": 39,
    "instack": 75,
    "warehouse": [
      { "location": "surat", "quntity": 26 },
      { "location": "lanavala", "quntity": 17 }
    ]
  }
]
```

#### 3.3 **Output of `db.item.find({ $or: [{ status: "A" }, { "warehouse.quntity": { $lt: 30 }, height: { $gt: 10 } }] })`**
```json
[
  {
    "_id": ObjectId("..."),
    "itemName": "planner",
    "tag": ["wash", "food", "vehicle"],
    "status": "A",
    "height": 5,
    "width": 9,
    "instack": 15,
    "warehouse": [
      { "location": "pune", "quntity": 36 },
      { "location": "mumbai", "quntity": 67 }
    ]
  },
  {
    "_id": ObjectId("..."),
    "itemName": "roboticcar",
    "tag": ["food", "vehicle"],
    "status": "A",
    "height": 9,
    "width": 9,
    "instack": 5,
    "warehouse": [
      { "location": "pune", "quntity": 26 },
      { "location": "mumbai", "quntity": 17 }
    ]
  }
]
```

#### 3.4 **Output of `db.item.find({ itemName: "planner", instack: { $lt: 20 } })`**
```json
[
  {
    "_id": ObjectId("..."),
    "itemName": "planner",
    "tag": ["wash", "food", "vehicle"],
    "status": "A",
    "height": 5,
    "width": 9,
    "instack": 15,
    "warehouse": [
      { "location": "pune", "quntity": 36 },
      { "location": "mumbai", "quntity": 67 }
    ]
  }
]
```

---

### 4. **Explanation of Query Operators**

- **$gt**: This operator is used to find values greater than a specified value (e.g., `quntity: { $gt: 30 }`).
- **$size**: This operator checks the size of an array (e.g., `{ $size: 3 }`).
- **$or**: This operator allows combining multiple conditions, where at least one condition must match.
- **$lt**: This operator is used to find values less than a specified value (e.g., `instack: { $lt: 20 }`).

---

These queries can help manage and retrieve data from an `item` collection efficiently based on specific criteria, such as item status, quantity, or tags.
