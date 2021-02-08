### MongoDB Example for Hospital Information

In this example, we'll manage information related to hospitals, their specializations, doctors, and patient ratings. The data will be stored in a **Hospital** collection, and we'll perform several MongoDB queries to extract specific information.

### 1. **Setting up Collections and Data**

#### 1.1 **Create the `Hospital` Database**
```javascript
use Hospital
```

#### 1.2 **Inserting Data into the `Hospital` Collection**
The `Hospital` collection stores hospital information such as the hospital number, name, specializations, people (patients) with ratings, and doctor visit schedules.

```javascript
db.Hospital.insert({
  Hno: 1, Hname: "AAA", Specialization: ["Pediatric", "Gynaec", "Orthopaedic"],
  People: [{ Pname: "PQR", Rating: 4 }, { Pname: "SDE", Rating: 5 }],
  Doctor: [{ Dname: "WWW", Visit: "Sunday" }]
})

db.Hospital.insert({
  Hno: 2, Hname: "BBB", Specialization: ["Gynaec", "Orthopaedic"],
  People: [{ Pname: "POP", Rating: 2 }, { Pname: "SDE", Rating: 3 }],
  Doctor: [{ Dname: "XXX", Visit: "Monday" }]
})

db.Hospital.insert({
  Hno: 3, Hname: "CCC", Specialization: ["Gynaec", "Orthopaedic", "Pediatric"],
  People: [{ Pname: "KLO", Rating: 3 }, { Pname: "LPO", Rating: 3 }],
  Doctor: [{ Dname: "XXX", Visit: "Tuesday" }]
})

db.Hospital.insert({
  Hno: 4, Hname: "DDD", Specialization: ["bones", "Gynaec", "Orthopaedic"],
  People: [{ Pname: "kunal", Rating: 4 }, { Pname: "Rohan", Rating: 5 }],
  Doctor: [{ Dname: "WWW", Visit: "Monday" }]
})

db.Hospital.insert({
  Hno: 5, Hname: "EEE", Specialization: ["Skin", "Gynaec", "Orthopaedic"],
  People: [{ Pname: "mohit", Rating: 4 }, { Pname: "mayur", Rating: 5 }],
  Doctor: [{ Dname: "WWW", Visit: "Sunday" }]
})

db.Hospital.insert({
  Hno: 6, Hname: "FF", Specialization: ["Pediatric", "Gynaec", "Orthopaedic"],
  People: [{ Pname: "sushant", Rating: 4 }, { Pname: "Bhai", Rating: 5 }],
  Doctor: [{ Dname: "WWW", Visit: "Sunday" }]
})

db.Hospital.insert({
  Hno: 7, Hname: "GG", Specialization: ["Pediatric", "Gynaec", "Orthopaedic"],
  People: [{ Pname: "hrushi", Rating: 2 }, { Pname: "SDE", Rating: 3 }],
  Doctor: [{ Dname: "XXX", Visit: "Monday" }]
})

db.Hospital.insert({
  Hno: 8, Hname: "HH", Specialization: ["Gynaec", "Orthopaedic", "Pediatric"],
  People: [{ Pname: "sahil", Rating: 3 }, { Pname: "LPO", Rating: 3 }],
  Doctor: [{ Dname: "XXX", Visit: "Tuesday" }]
})

db.Hospital.insert({
  Hno: 9, Hname: "II", Specialization: ["bones", "Gynaec", "Orthopaedic"],
  People: [{ Pname: "kunal", Rating: 4 }, { Pname: "Rohan", Rating: 3 }],
  Doctor: [{ Dname: "WWW", Visit: "Monday" }]
})

db.Hospital.insert({
  Hno: 10, Hname: "JJ", Specialization: ["Skin", "Gynaec", "Orthopaedic"],
  People: [{ Pname: "mohit", Rating: 4 }, { Pname: "mayur", Rating: 4 }],
  Doctor: [{ Dname: "WWW", Visit: "Sunday" }]
})
```

---

### 2. **Query Operations**

#### 2.1 **Find Hospitals with "Pediatric" Specialization**
This query finds all hospitals that have "Pediatric" in their list of specializations.

```javascript
db.Hospital.find({ Specialization: "Pediatric" })
```

#### 2.2 **Find Hospital "CCC" with Doctor Visit on "Tuesday"**
This query retrieves hospital "CCC" where the doctor visits on "Tuesday".

```javascript
db.Hospital.find({ Hname: "CCC", "Doctor.Visit": "Tuesday" })
```

#### 2.3 **Find Hospitals with More Than One Specialization and Doctor "XXX"**
This query finds hospitals that have more than one specialization and where the doctor is "XXX".

```javascript
db.Hospital.find({ Specialization: { $not: { $size: 1 } }, "Doctor.Dname": "XXX" })
```

#### 2.4 **Find Hospital "AAA" with Patients Rating Greater Than 3**
This query retrieves the hospital "AAA" where the patient's rating is greater than 3.

```javascript
db.Hospital.find({ "People.Rating": { $gt: 3 }, Hname: "AAA" })
```

---

### 3. **MongoDB Query Operators**

- **$not**: This operator is used to negate a condition. In the case of `{ $not: { $size: 1 } }`, it checks for hospitals with more than one specialization.
- **$size**: This operator is used to find documents where an array field has a specified number of elements. Here, it helps filter hospitals with more than one specialization.
- **$gt**: This operator checks if the value is greater than the specified value. It's used to filter patient ratings greater than 3.

---

### 4. **Sample Output**

#### 4.1 **Output of `db.Hospital.find({ Specialization: "Pediatric" })`**
```json
[
  { "_id": ObjectId("..."), "Hno": 1, "Hname": "AAA", "Specialization": ["Pediatric", "Gynaec", "Orthopaedic"], "People": [{ "Pname": "PQR", "Rating": 4 }, { "Pname": "SDE", "Rating": 5 }], "Doctor": [{ "Dname": "WWW", "Visit": "Sunday" }] },
  { "_id": ObjectId("..."), "Hno": 6, "Hname": "FF", "Specialization": ["Pediatric", "Gynaec", "Orthopaedic"], "People": [{ "Pname": "sushant", "Rating": 4 }, { "Pname": "Bhai", "Rating": 5 }], "Doctor": [{ "Dname": "WWW", "Visit": "Sunday" }] },
  { "_id": ObjectId("..."), "Hno": 7, "Hname": "GG", "Specialization": ["Pediatric", "Gynaec", "Orthopaedic"], "People": [{ "Pname": "hrushi", "Rating": 2 }, { "Pname": "SDE", "Rating": 3 }], "Doctor": [{ "Dname": "XXX", "Visit": "Monday" }] },
  { "_id": ObjectId("..."), "Hno": 8, "Hname": "HH", "Specialization": ["Gynaec", "Orthopaedic", "Pediatric"], "People": [{ "Pname": "sahil", "Rating": 3 }, { "Pname": "LPO", "Rating": 3 }], "Doctor": [{ "Dname": "XXX", "Visit": "Tuesday" }] }
]
```

#### 4.2 **Output of `db.Hospital.find({ Hname: "CCC", "Doctor.Visit": "Tuesday" })`**
```json
[
  { "_id": ObjectId("..."), "Hno": 3, "Hname": "CCC", "Specialization": ["Gynaec", "Orthopaedic", "Pediatric"], "People": [{ "Pname": "KLO", "Rating": 3 }, { "Pname": "LPO", "Rating": 3 }], "Doctor": [{ "Dname": "XXX", "Visit": "Tuesday" }] }
]
```

#### 4.3 **Output of `db.Hospital.find({ Specialization: { $not: { $size: 1 } }, "Doctor.Dname": "XXX" })`**
```json
[
  { "_id": ObjectId("..."), "Hno": 3, "Hname": "CCC", "Specialization": ["Gynaec", "Orthopaedic", "Pediatric"], "People": [{ "Pname": "KLO", "Rating": 3 }, { "Pname": "LPO", "Rating": 3 }], "Doctor": [{ "Dname": "XXX", "Visit": "Tuesday" }] },
  { "_id": ObjectId("..."), "Hno": 7, "Hname": "GG", "Specialization": ["Pediatric", "Gynaec", "Orthopaedic"], "People": [{ "Pname": "hrushi", "Rating": 2 }, { "Pname": "SDE", "Rating": 3 }], "Doctor": [{ "Dname": "XXX", "Visit": "Monday" }] }
]
```

#### 4.4 **Output of `db.Hospital.find({ "People.Rating": { $gt: 3 }, Hname: "AAA" })`**
```json
[
  { "_id": ObjectId("..."), "Hno": 1, "Hname": "AAA", "Specialization": ["Pediatric", "Gynaec", "Orthopaedic"], "People": [{ "Pname": "PQR", "Rating": 4 }, { "Pname": "SDE", "Rating": 5 }], "Doctor": [{ "Dname": "WWW", "Visit": "Sunday" }] }
]
```

---

### 5. **Conclusion**

This example demonstrates how to manage hospital data, including details about specializations, doctors, and patient ratings, using MongoDB. We performed several queries to filter hospitals based on different conditions, such as specialization, doctor visit schedule, and patient ratings.
