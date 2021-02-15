Here are the **MongoDB queries** you can use for managing and querying **`transaction`** data, such as transactions made by customers, their payment modes, and total payments.

### 1. **Setting Up the Database and Collection**

#### 1.1 **Create the `transaction` Database**
```javascript
use transaction
```

#### 1.2 **Inserting Data into the `transaction` Collection**
The data contains transactions with fields such as `itemName`, `customerName`, `paymentmode`, and `payment` amount.

```javascript
db.transaction.insert({ itemName: "toy", customerName: "john", paymentmode: "debitcard", payment: 8000 })
db.transaction.insert({ itemName: "car", customerName: "john", paymentmode: "creditcard", payment: 4000 })
db.transaction.insert({ itemName: "bag", customerName: "mukesh", paymentmode: "cash", payment: 5000 })
db.transaction.insert({ itemName: "airlineticket", customerName: "rohit", paymentmode: "cash", payment: 50090 })
db.transaction.insert({ itemName: "mango", customerName: "abhijeet", paymentmode: "creditcard", payment: 8000 })
db.transaction.insert({ itemName: "bus", customerName: "manasi", paymentmode: "debitcard", payment: 7000 })
```

---

### 2. **Query Operations**

#### 2.1 **Find All Transactions for a Specific Customer (e.g., "john")**
This query retrieves all transactions made by the customer **"john"**.

```javascript
db.transaction.find({ customerName: "john" })
```

#### 2.2 **Find All Transactions with Debit Card as the Payment Mode**
This query retrieves all transactions where the **payment mode is debitcard**.

```javascript
db.transaction.find({ paymentmode: "debitcard" })
```

#### 2.3 **Find the Total Payment Made by Credit Card Users**
This query uses an aggregation pipeline to find the total payment made by users who used **creditcard** as the payment mode.

```javascript
db.transaction.aggregate([
  { $match: { "paymentmode": "creditcard" } },
  { $group: { _id: null, "totalPayment": { $sum: "$payment" } } }
])
```

#### 2.4 **Find the Total Payment Grouped by Payment Mode**
This query aggregates the total payment amounts grouped by **payment mode** (e.g., cash, creditcard, debitcard).

```javascript
db.transaction.aggregate([
  { $group: { _id: "$paymentmode", "totalPayment": { $sum: "$payment" } } }
])
```

---

### 3. **Sample Outputs**

#### 3.1 **Output of `db.transaction.find({ customerName: "john" })`**
```json
[
  {
    "_id": ObjectId("..."),
    "itemName": "toy",
    "customerName": "john",
    "paymentmode": "debitcard",
    "payment": 8000
  },
  {
    "_id": ObjectId("..."),
    "itemName": "car",
    "customerName": "john",
    "paymentmode": "creditcard",
    "payment": 4000
  }
]
```

#### 3.2 **Output of `db.transaction.find({ paymentmode: "debitcard" })`**
```json
[
  {
    "_id": ObjectId("..."),
    "itemName": "toy",
    "customerName": "john",
    "paymentmode": "debitcard",
    "payment": 8000
  },
  {
    "_id": ObjectId("..."),
    "itemName": "bus",
    "customerName": "manasi",
    "paymentmode": "debitcard",
    "payment": 7000
  }
]
```

#### 3.3 **Output of `db.transaction.aggregate([{ $match: { "paymentmode": "creditcard" } }, { $group: { _id: null, "totalPayment": { $sum: "$payment" } } }])`**
```json
[
  {
    "_id": null,
    "totalPayment": 12000
  }
]
```

#### 3.4 **Output of `db.transaction.aggregate([{ $group: { _id: "$paymentmode", "totalPayment": { $sum: "$payment" } } }])`**
```json
[
  {
    "_id": "debitcard",
    "totalPayment": 15000
  },
  {
    "_id": "creditcard",
    "totalPayment": 12000
  },
  {
    "_id": "cash",
    "totalPayment": 55090
  }
]
```

---

### 4. **Explanation of Query Operators and Methods**

- **`$match`**: This stage in an aggregation pipeline filters documents to match specific criteria (e.g., `paymentmode: "creditcard"`).
- **`$group`**: This stage groups documents by a specified key and performs aggregate operations such as summing the values (e.g., `totalPayment: { $sum: "$payment" }`).
- **`$sum`**: This operator calculates the sum of a field for all documents in a group.

---

These queries will allow you to retrieve and analyze transaction data effectively, such as grouping payments by payment mode, filtering transactions by customer, and calculating total payments for specific payment methods.
