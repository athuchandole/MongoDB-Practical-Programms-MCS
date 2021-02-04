### MongoDB Blog Database Example

In this example, we will create and manage a **blog post** database with various attributes like title, URL, tags, user comments, and likes. We will perform a series of queries to extract specific blog post information based on different criteria.

### 1. **Setting Up the Database and Collections**

#### 1.1 **Create the `post` Database**
```javascript
use post
```

#### 1.2 **Inserting Data into the `post` Collection**
The `post` collection will contain blog posts with information like title, URL, tags, post name (author), post date, likes, and user comments.

```javascript
db.post.insert({
  title: "online",
  url: "www.abc.com",
  tag: ["food", "travel"],
  pname: "mukesh",
  pdate: new Date("2019-03-12"),
  like: 89,
  user: [{
    name: "abhi",
    comment: "good",
    message: "do best",
    cdate: new Date("2020-03-12"),
    like: 1
  }]
})

db.post.insert({
  title: "wetpet",
  url: "www.wetpet.com",
  tag: ["food", "travel"],
  pname: "Amit",
  pdate: new Date("2018-03-12"),
  like: 82,
  user: [
    { name: "abhi", comment: "good", message: "do best", time: "4pm", like: 1 },
    { name: "mukesh", comment: "best", message: "success", cdate: new Date("2008-11-12"), like: 2 }
  ]
})

db.post.insert({
  title: "wetpet",
  url: "www.wetpet.com",
  tag: ["food", "travel", "magic"],
  pname: "abhijeet",
  pdate: new Date("2017-03-12"),
  like: 182,
  user: [
    { name: "sagar", comment: "like", message: "dobest", time: "4pm", like: 1 },
    { name: "mukesh", comment: "best", message: "success", cdate: new Date("2019-03-12"), like: 2 }
  ]
})

db.post.insert({
  title: "nonveg",
  url: "www.non.com",
  tag: ["food", "travel", "chiken"],
  pname: "Amit",
  pdate: new Date("2019-07-12"),
  like: 82,
  user: [
    { name: "manisha", comment: "good", message: "dobest", time: "4pm", like: 0 },
    { name: "manasi", comment: "best", message: "success", cdate: new Date("2018-03-12"), like: 0 }
  ]
})
```

---

### 2. **Query Operations**

#### 2.1 **Find Posts with Tag "food"**
This query retrieves all blog posts that are tagged with "food".

```javascript
db.post.find({ tag: "food" })
```

#### 2.2 **Find Posts by Author "Amit"**
This query finds all blog posts written by the author "Amit".

```javascript
db.post.find({ pname: "Amit" })
```

#### 2.3 **Find Posts Tagged "travel", Date Before or Equal to "2018-03-11", and User "sagar" with Comment "like"**
This query retrieves blog posts tagged with "travel", where the post date is before or equal to "2018-03-11", and includes a comment by user "sagar" with the comment "like".

```javascript
db.post.find({
  tag: "travel",
  pdate: { "$lte": new Date("2018-03-11") },
  "user.name": "sagar",
  "user.comment": "like"
})
```

#### 2.4 **Find Posts Where Any User's Comment Date is Before or Equal to "2019-08-07", or the User's Like is 0**
This query finds blog posts where either any user's comment date is before or equal to "2019-08-07", or the user's like is 0.

```javascript
db.post.find({
  $or: [
    { "user.cdate": { $lte: new Date("2019-08-07") } },
    { "user.like": 0 }
  ]
})
```

---

### 3. **MongoDB Query Operators**

- **$lte**: The `$lte` operator is used to select documents where the value of a field is less than or equal to the specified value.
- **$or**: The `$or` operator is used to query documents where at least one of the given conditions is true.
- **Array Querying**: MongoDB allows querying for documents based on the presence of values in arrays. Here, `tag: "food"` and `user.name: "sagar"` are examples of how to query for values within array fields.

---

### 4. **Sample Output**

#### 4.1 **Output of `db.post.find({ tag: "food" })`**
```json
[
  {
    "_id": ObjectId("..."),
    "title": "online",
    "url": "www.abc.com",
    "tag": ["food", "travel"],
    "pname": "mukesh",
    "pdate": ISODate("2019-03-12T00:00:00.000Z"),
    "like": 89,
    "user": [{
      "name": "abhi",
      "comment": "good",
      "message": "do best",
      "cdate": ISODate("2020-03-12T00:00:00.000Z"),
      "like": 1
    }]
  },
  {
    "_id": ObjectId("..."),
    "title": "wetpet",
    "url": "www.wetpet.com",
    "tag": ["food", "travel"],
    "pname": "Amit",
    "pdate": ISODate("2018-03-12T00:00:00.000Z"),
    "like": 82,
    "user": [
      { "name": "abhi", "comment": "good", "message": "do best", "time": "4pm", "like": 1 },
      { "name": "mukesh", "comment": "best", "message": "success", "cdate": ISODate("2008-11-12T00:00:00.000Z"), "like": 2 }
    ]
  },
  {
    "_id": ObjectId("..."),
    "title": "wetpet",
    "url": "www.wetpet.com",
    "tag": ["food", "travel", "magic"],
    "pname": "abhijeet",
    "pdate": ISODate("2017-03-12T00:00:00.000Z"),
    "like": 182,
    "user": [
      { "name": "sagar", "comment": "like", "message": "dobest", "time": "4pm", "like": 1 },
      { "name": "mukesh", "comment": "best", "message": "success", "cdate": ISODate("2019-03-12T00:00:00.000Z"), "like": 2 }
    ]
  },
  {
    "_id": ObjectId("..."),
    "title": "nonveg",
    "url": "www.non.com",
    "tag": ["food", "travel", "chiken"],
    "pname": "Amit",
    "pdate": ISODate("2019-07-12T00:00:00.000Z"),
    "like": 82,
    "user": [
      { "name": "manisha", "comment": "good", "message": "dobest", "time": "4pm", "like": 0 },
      { "name": "manasi", "comment": "best", "message": "success", "cdate": ISODate("2018-03-12T00:00:00.000Z"), "like": 0 }
    ]
  }
]
```

#### 4.2 **Output of `db.post.find({ pname: "Amit" })`**
```json
[
  {
    "_id": ObjectId("..."),
    "title": "wetpet",
    "url": "www.wetpet.com",
    "tag": ["food", "travel"],
    "pname": "Amit",
    "pdate": ISODate("2018-03-12T00:00:00.000Z"),
    "like": 82,
    "user": [
      { "name": "abhi", "comment": "good", "message": "do best", "time": "4pm", "like": 1 },
      { "name": "mukesh", "comment": "best", "message": "success", "cdate": ISODate("2008-11-12T00:00:00.000Z"), "like": 2 }
    ]
  },
  {
    "_id": ObjectId("..."),
    "title": "nonveg",
    "url": "www.non.com",
    "tag": ["food", "travel", "chiken"],
    "pname": "Amit",
    "pdate": ISODate("2019-07-12T00:00:00.000Z"),
    "like": 82,
    "user": [
      { "name": "manisha", "comment": "good", "message": "dobest", "time": "4pm", "like": 0 },
      { "name": "manasi", "comment": "best", "message": "success", "cdate": ISODate("2018-03-12T00:00:00.000Z"), "like": 0 }
    ]
  }
]
```

#### 4.3 **Output of `db.post.find({ tag: "travel", pdate: { "$lte": new Date("2018-03-11") }, "user.name": "sagar", "user.comment": "like" })`**
```json
[
  {
    "_id": ObjectId("..."),
    "title": "wetpet",
    "url": "www.wetpet.com",
    "tag": ["food", "travel", "magic"],
    "pname": "abhijeet",
    "pdate": ISODate("2017-03-12T00:00:00.000Z"),
    "like": 182,
    "user": [
      { "name": "sagar", "comment": "like", "message": "dobest", "time": "4pm", "like": 1 },
      { "name": "mukesh", "comment": "best", "message": "success", "cdate": ISODate("2019-03-12T00:00:00.000Z"), "like": 2 }
    ]
  }
]
```

---

### 5. **Conclusion**

This example demonstrates how to create and query a MongoDB database that stores blog posts, user comments, and likes. The queries allow you to filter posts by tags, authors, specific comments, and more.
