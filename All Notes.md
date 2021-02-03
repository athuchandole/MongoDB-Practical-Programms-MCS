Got it! You want to create a `.md` file that maintains the same structure and allows easy copying and pasting. Here's how you can structure it in a Markdown file for easy copy-pasting, preserving the format:

```markdown
## Q. student

```bash
use student
db.student.insert({name:"Athu",course:[{coursename:"mcs"},{coursename:"bcs"}],marks:80,age:21,gender:"male",city:"nashik"})
db.student.insert({name:"Kalpesh",course:[{coursename:"mcs"},{coursename:"bcs"}],marks:95,age:20,gender:"male",city:"sinner"})
db.student.insert({name:"Shijuka",course:[{coursename:"iti"},{coursename:"bcs"}],marks:40,age:18,gender:"female",city:"pune"})
db.student.insert({name:"payal",course:[{coursename:"chemistry"},{coursename:"mcs"}],marks:81,age:19,gender:"female",city:"mumbai"})
db.student.insert({name:"sushant",course:[{coursename:"iti"},{coursename:"bsc"}],marks:35,age:19,gender:"male",city:"sinner"})
db.student.insert({name:"anushka",course:[{coursename:"msc"},{coursename:"bcs"}],marks:90,age:21,gender:"female",city:"pune"})
db.student.insert({name:"aditya",course:[{coursename:"msc"},{coursename:"bcs"}],marks:50,age:21,gender:"male",city:"nashik"})
db.student.insert({name:"Amit",course:[{coursename:"msc"},{coursename:"bcs"}],marks:50,age:21,gender:"male",city:"mumbai"})
db.student.insert({name:"amol",course:[{coursename:"msc"},{coursename:"bcs"}],marks:35,age:21,gender:"male",city:"mumbai"})
db.student.insert({name:"praju",course:[{coursename:"msc"},{coursename:"bcs"}],marks:39,age:21,gender:"female",city:"mumbai"})
db.student.insert({name:"pratik",course:[{coursename:"msc"},{coursename:"bcs"}],marks:63,age:21,gender:"male",city:"mumbai"})

db.student.count({marks:{$gt:80}})
db.student.find({marks:{$lt:40}})
var my=db.student.find({marks:{$gt:70}});
while(my.hasNext()){print(tojson(my.next()));}
db.student.find({gender:"female",$or:[{city:"pune"},{city:"mumbai"},{marks:{$lt:50}}]})
```

## Q products, customers, orders and invoices.

```bash
use product
db.product.insert({name:"robot",price:12000})
db.product.insert({name:"toycar",price:2000})
db.product.insert({name:"cricketset",price:9000})
db.product.insert({name:"studymaterial",price:19000})
db.order.insert({orderno:3736,custName:"arun kumar",product:{productName:"toycar",price:20000},order_date:"12/2/2019",stetus:"processed",Totalbill:2039,invoice:{invoiceNO:67564,bill:2039,date:"17/2/2019"}})
db.order.insert({orderno:3737,custName:"arun kumar",product:{productName:"robot",price:12000},order_date:"11/3/2019",stetus:"processed",Totalbill:12800,invoice:{invoiceNO:67574,bill:12039,date:"17/3/2019"}})
db.order.insert({orderno:3738,custName:"arun kumar",product:{productName:"cricketset",price:9000},order_date:"15/5/2019",stetus:"in process",Totalbill:9050})
db.order.insert({orderno:3739,custName:"mukesh patil",product:{productName:"studentmaterial",price:19000},order_date:"15/8/2019",stetus:"in process",Totalbill:19080})

db.product.find().pretty()
db.order.find({Totalbill:{$lt:10000}})
db.order.find({stetus:"in process"})
db.order.find({custName:"arun kumar",stetus:"processed"})
```

## Q books and publishers

```bash
use book
db.book.insert({BName:"shyamchiaai",cost:500,author:"sane guruji",published:2005})
db.book.insert({BName:"Two Saints",cost:2000,author:"raguramkrishna",published:2015})
db.book.insert({BName:"ramkrushnaparamhans",cost:1000,author:"raguramkrishna",published:2020})
db.book.insert({BName:"DMS",cost:100,author:"raguramkrishna",published:2007})
db.publisher.insert({pname:"OReilly",language:"English",books:[{BName:"ramkrushnaparamhans"},{BName:"Two Saints"}],city:"mumbai"})
db.publisher.insert({pname:"vision",language:"English",books:[{BName:"DMS"}],city:"pune"})
db.publisher.insert({pname:"OReilly",language:"marathi",books:[{BName:"shyamchiaai"}],city:"mumbai"})

db.publisher.find({city:"mumbai"})
db.book.find({cost:{$lt:1000}})
db.book.find({author:"raguramkrishna",published:2017})
db.publisher.find({pname:"OReilly",$or:[{language:"English"},{language:"marathi"}]})
```

## Q Hospital information

```bash
use Hospital
db.Hospital.insert({Hno:1,Hname:"AAA",Specialization:["Pediatric","Gynaec","Orthopaedic"],People:[{Pname:"PQR",Rating:4},{Pname:"SDE",Rating:5}],Doctor:[{"Dname":"WWW","Visit":"Sunday"}]})
db.Hospital.insert({Hno:2,Hname:"BBB",Specialization:["Gynaec","Orthopaedic"],People:[{Pname:"POP",Rating:2},{Pname:"SDE",Rating:3}],Doctor:[{"Dname":"XXX",Visit:"Monday"}]})
db.Hospital.insert({Hno:3,Hname:"CCC",Specialization:["Gynaec","Orthopaedic","Pediatric"],People:[{Pname:"KLO",Rating:3},{Pname:"LPO",Rating:3}],Doctor:[{"Dname":"XXX","Visit":"Tuesday"}]})
db.Hospital.insert({Hno:4,Hname:"DDD",Specialization:["bones","Gynaec","Orthopaedic"],People:[{Pname:"kunal",Rating:4},{Pname:"Rohan",Rating:5}],Doctor:[{"Dname":"WWW","Visit":"Monday"}]})
db.Hospital.insert({Hno:5,Hname:"EEE",Specialization:["Skin","Gynaec","Orthopaedic"],People:[{Pname:"mohit",Rating:4},{Pname:"mayur",Rating:5}],Doctor:[{"Dname":"WWW","Visit":"Sunday"}]})
db.Hospital.insert({Hno:6,Hname:"FF",Specialization:["Pediatric","Gynaec","Orthopaedic"],People:[{Pname:"sushant",Rating:4},{Pname:"Bhai",Rating:5}],Doctor:[{"Dname":"WWW","Visit":"Sunday"}]})
db.Hospital.insert({Hno:7,Hname:"GG",Specialization:["Pediatric","Gynaec","Orthopaedic"],People:[{Pname:"hrushi",Rating:2},{Pname:"SDE",Rating:3}],Doctor:[{"Dname":"XXX",Visit:"Monday"}]})
db.Hospital.insert({Hno:8,Hname:"HH",Specialization:["Gynaec","Orthopaedic","Pediatric"],People:[{Pname:"sahil",Rating:3},{Pname:"LPO",Rating:3}],Doctor:[{"Dname":"XXX","Visit":"Tuesday"}]})
db.Hospital.insert({Hno:9,Hname:"II",Specialization:["bones","Gynaec","Orthopaedic"],People:[{Pname:"kunal",Rating:4},{Pname:"Rohan",Rating:3}],Doctor:[{"Dname":"WWW","Visit":"Monday"}]})
db.Hospital.insert({Hno:10,Hname:"JJ",Specialization:["Skin","Gynaec","Orthopaedic"],People:[{Pname:"mohit",Rating:4},{Pname:"mayur",Rating:4}],Doctor:[{"Dname":"WWW","Visit":"Sunday"}]})

db.Hospital.find({Specialization:"Pediatric"})
db.Hospital.find({Hname:"CCC","Doctor.Visit":"Tuesday"})
db.Hospital.find({Specialization:{$not:{$size:1}},"Doctor.Dname":"XXX"})
db.Hospital.find({"People.Rating":{$gt:3},Hname:"AAA"})
```

---

Continue this pattern for other queries as well.

For instance:
- Q blog database
- Q Tours information
- Q scientist information
- Q quantity of the item
- Q transaction information
- Q Mobile Shopping

By following this structure, the entire content can be formatted into Markdown, making it easy for anyone to copy and paste the code directly from the document into their MongoDB environment.
