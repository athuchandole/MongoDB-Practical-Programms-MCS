### MongoDB Scientist Database Example

In this example, we manage a **scientist** database, which includes information about scientists, their awards, fields of expertise, and birth/death dates. The database is stored in the `scien` collection.

### 1. **Setting Up the Database and Collection**

#### 1.1 **Create the `scien` Database**
```javascript
use scien
```

#### 1.2 **Inserting Data into the `scien` Collection**
We insert data for several scientists, including their first name (`fname`), last name (`lname`), date of birth (`BOD`), date of death (`DOD`), fields of expertise (`field`), and awards (`award`).

```javascript
db.scien.insert({
  fname: "mukesh",
  lname: "navse",
  BOD: new Date("1952-04-18"),
  DOD: "stillalive",
  field: ["tcs", "java", "c", "sql"],
  award: [
    { name: "turingmachine", year: 1976 },
    { name: "robotic", year: 1998 },
    { name: "code talent", year: 1995 }
  ]
})

db.scien.insert({
  fname: "abhi",
  lname: "nalave",
  BOD: new Date("1972-04-18"),
  DOD: "stillalive",
  field: ["tcs", "java", "sql"],
  award: [
    { name: "codemaster", year: 1976 },
    { name: "robot", year: 1998 },
    { name: "puzzletalent", year: 1995 }
  ]
})

db.scien.insert({
  fname: "manisha",
  lname: "hipparkar",
  BOD: new Date("1942-04-18"),
  DOD: new Date("2009-08-06"),
  field: ["tcs", "java"],
  award: [
    { name: "topper", year: 1976 },
    { name: "puraskar", year: 1998 },
    { name: "puzzletalent", year: 1995 }
  ]
})
```

---

### 2. **Query Operations**

#### 2.1 **Find Scientists with Last Name Containing the Letter 'n'**
This query uses a regular expression (`$regex`) to find scientists whose last name contains the letter "n".

```javascript
db.scien.find({ lname: { $regex: /n/ } })
```

#### 2.2 **Find Scientists Born After March 11, 1950, and Still Alive**
This query looks for scientists whose date of birth is greater than a certain date and who are still alive (`DOD: "stillalive"`).

```javascript
db.scien.find({ BOD: { "$gt": new Date("1950-03-11") }, DOD: "stillalive" })
```

#### 2.3 **Group by Award Year and Name**
This query groups the scientists by the year and name of the awards they have received.

```javascript
db.scien.aggregate([
  { $unwind: "$award" },
  { $group: { _id: { year: "$award.year", Name: "$award.name" } } }
])
```

#### 2.4 **Find Scientists Who Won "Turingmachine" Award Before 1980 and Have Exactly 4 Fields of Expertise**
This query searches for scientists who won the "Turingmachine" award before 1980 and have exactly 4 fields of expertise.

```javascript
db.scien.find({
  "award.name": "turingmachine",
  "award.year": { $lt: 1980 },
  field: { $size: 4 }
})
```

---

### 3. **MongoDB Query Operators**

- **$regex**: Searches for a pattern in a field, useful for matching text (like partial names).
- **$gt**: Selects documents where the field's value is greater than the specified value.
- **$unwind**: Deconstructs an array field from the input documents, outputting a document for each element in the array.
- **$group**: Groups documents together based on specified criteria (in this case, by award year and name).
- **$size**: Matches arrays with a specified number of elements.

---

### 4. **Sample Output**

#### 4.1 **Output of `db.scien.find({ lname: { $regex: /n/ } })`**
```json
[
  {
    "_id": ObjectId("..."),
    "fname": "mukesh",
    "lname": "navse",
    "BOD": ISODate("1952-04-18T00:00:00Z"),
    "DOD": "stillalive",
    "field": ["tcs", "java", "c", "sql"],
    "award": [
      { "name": "turingmachine", "year": 1976 },
      { "name": "robotic", "year": 1998 },
      { "name": "code talent", "year": 1995 }
    ]
  },
  {
    "_id": ObjectId("..."),
    "fname": "abhi",
    "lname": "nalave",
    "BOD": ISODate("1972-04-18T00:00:00Z"),
    "DOD": "stillalive",
    "field": ["tcs", "java", "sql"],
    "award": [
      { "name": "codemaster", "year": 1976 },
      { "name": "robot", "year": 1998 },
      { "name": "puzzletalent", "year": 1995 }
    ]
  }
]
```

#### 4.2 **Output of `db.scien.find({ BOD: { "$gt": new Date("1950-03-11") }, DOD: "stillalive" })`**
```json
[
  {
    "_id": ObjectId("..."),
    "fname": "abhi",
    "lname": "nalave",
    "BOD": ISODate("1972-04-18T00:00:00Z"),
    "DOD": "stillalive",
    "field": ["tcs", "java", "sql"],
    "award": [
      { "name": "codemaster", "year": 1976 },
      { "name": "robot", "year": 1998 },
      { "name": "puzzletalent", "year": 1995 }
    ]
  }
]
```

#### 4.3 **Output of `db.scien.aggregate([ { $unwind: "$award" }, { $group: { _id: { year: "$award.year", Name: "$award.name" } } } ])`**
```json
[
  { "_id": { "year": 1976, "Name": "turingmachine" } },
  { "_id": { "year": 1998, "Name": "robotic" } },
  { "_id": { "year": 1995, "Name": "code talent" } },
  { "_id": { "year": 1976, "Name": "codemaster" } },
  { "_id": { "year": 1998, "Name": "robot" } },
  { "_id": { "year": 1995, "Name": "puzzletalent" } },
  { "_id": { "year": 1976, "Name": "topper" } },
  { "_id": { "year": 1998, "Name": "puraskar" } }
]
```

#### 4.4 **Output of `db.scien.find({ "award.name": "turingmachine", "award.year": { $lt: 1980 }, field: { $size: 4 } })`**
```json
[
  {
    "_id": ObjectId("..."),
    "fname": "mukesh",
    "lname": "navse",
    "BOD": ISODate("1952-04-18T00:00:00Z"),
    "DOD": "stillalive",
    "field": ["tcs", "java", "c", "sql"],
    "award": [
      { "name": "turingmachine", "year": 1976 },
      { "name": "robotic", "year": 1998 },
      { "name": "code talent", "year": 1995 }
    ]
  }
]
```

---

### 5. **Conclusion**

This example demonstrates how to manage and query a MongoDB database for scientist information, including their awards, fields of expertise, and birth/death dates. The queries show how to retrieve information based on specific criteria, such as finding scientists by their last name or award information, filtering by birth or death date, or aggregating awards by year and name.
