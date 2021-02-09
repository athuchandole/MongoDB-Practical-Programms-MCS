### MongoDB Example for Products, Orders, and Invoices

In this example, we'll set up a database with **Products**, **Orders**, and **Invoices** collections. We will perform several MongoDB operations like inserting documents, querying data, and using operators.

### 1. **Setting up Collections and Data**

#### 1.1 **Create the `product` Database**
```javascript
use product
```

#### 1.2 **Inserting Data into the `product` Collection**
This collection stores the products with their names and prices.

```javascript
db.product.insert({ name: "robot", price: 12000 })
db.product.insert({ name: "toycar", price: 2000 })
db.product.insert({ name: "cricketset", price: 9000 })
db.product.insert({ name: "studymaterial", price: 19000 })
```

#### 1.3 **Inserting Data into the `order` Collection**
The `order` collection tracks customer orders, with information like the order number, customer name, product details, order date, order status, total bill, and invoice details.

```javascript
db.order.insert({
  orderno: 3736,
  custName: "arun kumar",
  product: { productName: "toycar", price: 20000 },
  order_date: "12/2/2019",
  stetus: "processed",
  Totalbill: 2039,
  invoice: { invoiceNO: 67564, bill: 2039, date: "17/2/2019" }
})

db.order.insert({
  orderno: 3737,
  custName: "arun kumar",
  product: { productName: "robot", price: 12000 },
  order_date: "11/3/2019",
  stetus: "processed",
  Totalbill: 12800,
  invoice: { invoiceNO: 67574, bill: 12039, date: "17/3/2019" }
})

db.order.insert({
  orderno: 3738,
  custName: "arun kumar",
  product: { productName: "cricketset", price: 9000 },
  order_date: "15/5/2019",
  stetus: "in process",
  Totalbill: 9050
})

db.order.insert({
  orderno: 3739,
  custName: "mukesh patil",
  product: { productName: "studymaterial", price: 19000 },
  order_date: "15/8/2019",
  stetus: "in process",
  Totalbill: 19080
})
```

---

### 2. **Query Operations**

#### 2.1 **Find All Products**
To view all products in the `product` collection:

```javascript
db.product.find().pretty()
```

This will return a list of all the products with their respective prices.

#### 2.2 **Find Orders with Total Bill Less Than 10,000**
This query finds orders with a `Totalbill` less than 10,000:

```javascript
db.order.find({ Totalbill: { $lt: 10000 } })
```

#### 2.3 **Find Orders with Status "In Process"**
This query returns all orders that are currently "in process":

```javascript
db.order.find({ stetus: "in process" })
```

#### 2.4 **Find Orders for a Specific Customer (arun kumar) with "Processed" Status**
This query retrieves all orders made by the customer `arun kumar` that have a status of "processed":

```javascript
db.order.find({ custName: "arun kumar", stetus: "processed" })
```

---

### 3. **MongoDB Query Operators**

- **$lt (Less Than)**: Used to query for values less than a specified number (e.g., `Totalbill: { $lt: 10000 }`).
- **Pretty()**: Used to format the output of a query to make it more readable.

---

### 4. **Sample Output**

#### 4.1 **Output of `db.product.find().pretty()`**
```json
[
  { "_id": ObjectId("..."), "name": "robot", "price": 12000 },
  { "_id": ObjectId("..."), "name": "toycar", "price": 2000 },
  { "_id": ObjectId("..."), "name": "cricketset", "price": 9000 },
  { "_id": ObjectId("..."), "name": "studymaterial", "price": 19000 }
]
```

#### 4.2 **Output of `db.order.find({ Totalbill: { $lt: 10000 } })`**
```json
[
  { "_id": ObjectId("..."), "orderno": 3736, "custName": "arun kumar", "product": { "productName": "toycar", "price": 20000 }, "order_date": "12/2/2019", "stetus": "processed", "Totalbill": 2039, "invoice": { "invoiceNO": 67564, "bill": 2039, "date": "17/2/2019" } },
  { "_id": ObjectId("..."), "orderno": 3738, "custName": "arun kumar", "product": { "productName": "cricketset", "price": 9000 }, "order_date": "15/5/2019", "stetus": "in process", "Totalbill": 9050 }
]
```

#### 4.3 **Output of `db.order.find({ stetus: "in process" })`**
```json
[
  { "_id": ObjectId("..."), "orderno": 3738, "custName": "arun kumar", "product": { "productName": "cricketset", "price": 9000 }, "order_date": "15/5/2019", "stetus": "in process", "Totalbill": 9050 },
  { "_id": ObjectId("..."), "orderno": 3739, "custName": "mukesh patil", "product": { "productName": "studymaterial", "price": 19000 }, "order_date": "15/8/2019", "stetus": "in process", "Totalbill": 19080 }
]
```

#### 4.4 **Output of `db.order.find({ custName: "arun kumar", stetus: "processed" })`**
```json
[
  { "_id": ObjectId("..."), "orderno": 3736, "custName": "arun kumar", "product": { "productName": "toycar", "price": 20000 }, "order_date": "12/2/2019", "stetus": "processed", "Totalbill": 2039, "invoice": { "invoiceNO": 67564, "bill": 2039, "date": "17/2/2019" } },
  { "_id": ObjectId("..."), "orderno": 3737, "custName": "arun kumar", "product": { "productName": "robot", "price": 12000 }, "order_date": "11/3/2019", "stetus": "processed", "Totalbill": 12800, "invoice": { "invoiceNO": 67574, "bill": 12039, "date": "17/3/2019" } }
]
```

---

### 5. **Conclusion**
This example demonstrates how to use MongoDB for storing and querying information about products, orders, and invoices. The operations include inserting documents, querying with conditions, and formatting the results for better readability.

--- 

This structure provides a complete overview of how to manage product, order, and invoice data in MongoDB.
