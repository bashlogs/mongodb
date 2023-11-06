---
description: >-
  In my MongoDB documentation, I am practicing various operations and commands
  to interact with a MongoDB database named "school." Here's a breakdown of the
  context for each section of my documentation
---

# MongoDB Documentation
### In my MongoDB documentation, I am practicing various operations and commands to interact with a MongoDB database named "school." Here's a breakdown of the context for each section of my documentation

## Connection:

* Connection string: `mongosh "mongodb+srv://cluster0.k3uephw.mongodb.net/" --apiVersion 1 --username mayur`
* Password: JE5lyxzuYC58XHWs

## Database:

* Show available databases: `show dbs`
* Switch to the "school" database: `use school`
* Create a collection named "students": `db.createCollection("students")`
* Drop the "school" database: `db.dropDatabase()`

## Insert:

*   Insert a single document:

    ```javascript
    javascriptCopy codedb.students.insertOne({name: "Mayur Khadde", age: 30, gpa: 3.2})
    ```


*   Insert multiple documents:

    ```javascript
    javascriptCopy codedb.students.insertMany([
      {name: "Patrick", age: 38, gpa: 1.5},
      {name: "Sandy", age: 27, gpa: 4.0},
      {name: "Gary", age: 18, gpa: 2.5}
    ])
    ```


*   Insert a complex document:

    ```javascript
    javascriptCopy codedb.students.insertOne({
      name: "Larry 123",
      age: 32,
      gpa: 2.8,
      fullTime: true,
      registerDate: new Date("2023-01-02"),
      gradutionDate: null,
      courses: ["Biology", "Chemistry", "Calculus"],
      address: {
        Street: "123 Fake St.",
        city: "Bikini Bottom",
        zip: 12345
      }
    })
    ```

## Find:

*   Find all students, sorted by name in descending order:

    ```javascript
    javascriptCopy codedb.students.find().sort({name: -1})
    ```


*   Find all students, sorted by GPA in ascending order:

    ```javascript
    javascriptCopy codedb.students.find().sort({gpa: 1})
    ```


*   Find the first student:

    ```javascript
    javascriptCopy codedb.students.find().limit(1)
    ```


*   Find the student with the highest GPA:

    ```javascript
    javascriptCopy codedb.students.find().sort({gpa: -1}).limit(1)
    ```


*   Find a student by name:

    ```javascript
    javascriptCopy codedb.students.find({name: "Mayur"})
    ```


*   Find full-time students:

    ```javascript
    javascriptCopy codedb.students.find({fullTime: true})
    ```


*   Find all students, displaying only their names:

    ```javascript
    javascriptCopy codedb.students.find({}, {name: true})
    ```


*   Find all students, excluding the `_id` field, and displaying only their names:

    ```javascript
    javascriptCopy codedb.students.find({}, {_id: false, name: true})
    ```

## Update:

*   Update "Gary" to be a full-time student:

    ```javascript
    javascriptCopy codedb.students.updateOne({ name: "Gary" }, { $set: { fullTime: true } })
    ```


*   Find "Gary" to confirm the update:

    ```javascript
    javascriptCopy codedb.students.find({name: "Gary"})
    ```


*   Update a document by its `_id`:

    ```javascript
    javascriptCopy codedb.students.updateOne({ _id: ObjectId("6547d516fa269bcad3447d35") }, { $set: { fullTime: false } })
    ```


*   Unset the "fullTime" field in a document:

    ```javascript
    javascriptCopy codedb.students.updateOne({ _id: ObjectId("6547d516fa269bcad3447d35") }, { $unset: { fullTime: "" } })
    ```


*   Update all students to be non-full-time:

    ```javascript
    javascriptCopy codedb.students.updateMany({}, { $set: { fullTime: false } })
    ```


*   Unset the "fullTime" field for a student named "Tushar":

    ```javascript
    javascriptCopy codedb.students.updateOne({ name: "Tushar" }, { $unset: { fullTime: "" } })
    ```


*   Find the "Tushar" student to confirm the update:

    ```javascript
    javascriptCopy codedb.students.find({ name: "Tushar" })
    ```


*   Update all students without a "fullTime" field to be full-time:

    ```javascript
    javascriptCopy codedb.students.updateMany({ fullTime: { $exists: false } }, { $set: { fullTime: true } })
    ```


*   Find the "Tushar" student again to confirm the update:

    ```javascript
    javascriptCopy codedb.students.find({ name: "Tushar" })
    ```

## Delete:

*   Delete a single document by name:

    ```javascript
    javascriptCopy codedb.students.deleteOne({ name: "Tushar" })
    ```


*   Confirm that the "Tushar" student is deleted:

    ```javascript
    javascriptCopy codedb.students.find({ name: "Tushar" })
    ```


*   Delete all non-full-time students:

    ```javascript
    javascriptCopy codedb.students.deleteMany({ fullTime: false })
    ```

## Comparison Operator:

*   Find students with names other than "Mayur":

    ```javascript
    javascriptCopy codedb.students.find({ name: { $ne: "Mayur" } })
    ```


*   Find students with ages less than or equal to 30:

    ```javascript
    javascriptCopy codedb.students.find({ age: { $lte: 30 } })
    ```


*   Find students with ages greater than or equal to 27:

    ```javascript
    javascriptCopy codedb.students.find({ age: { $gte: 27 } })
    ```


*   Find students with GPAs between 3 and 4:

    ```javascript
    javascriptCopy codedb.students.find({ gpa: { $gte: 3, $lte: 4 } })
    ```


*   Find students with names "Mayur" or "Gary":

    ```javascript
    javascriptCopy codedb.students.find({ name: { $in: ["Mayur", "Gary"] } })
    ```


*   Find students with names other than "Mayur" or "Gary":

    ```javascript
    javascriptCopy codedb.students.find({ name: { $nin: ["Mayur", "Gary"] } })
    ```

## Logical Operator:

*   Find full-time students aged 22 or younger (AND condition):

    ```javascript
    javascriptCopy codedb.students.find({ $and: [{ fullTime: true }, { age: { $lte: 22 } }] })
    ```


*   Find students older than 30 (NOT condition):

    ```javascript
    javascriptCopy codedb.students.find({ age: { $not: { $gte: 30 } } })
    ```


*   Find non-full-time students or students aged 22 or younger (NOR condition):

    ```javascript
    javascriptCopy codedb.students.find({ $nor: [{ fullTime: true }, { age: { $lte: 22 } }] })
    ```


*   Find full-time students or students aged 22 or younger (OR condition):

    ```javascript
    javascriptCopy codedb.students.find({ $or: [{ fullTime: true }, { age: { $lte: 22 } }] })
    ```

## Index:

*   Perform a linear search for a student named "Larry":

    ```javascript
    javascriptCopy codedb.students.find({ name: "Larry" }).explain("executionStats")
    ```


*   Create an index on the "name" field:

    ```javascript
    javascriptCopy codedb.students.createIndex({ name: 1 })
    ```


*   Perform the same search with the new index:

    ```javascript
    javascriptCopy codedb.students.find({ name: "Larry" }).explain("executionStats")
    ```


*   Get the list of indexes on the "students" collection:

    ```javascript
    javascriptCopy codedb.students.getIndexes()
    ```


*   Drop the "name" index:

    ```javascript
    javascriptCopy codedb.students.dropIndex("name_1")
    ```

## Collections:

*   Show all collections in the current database:

    ```javascript
    javascriptCopy codeshow collections
    ```


*   Create a capped collection named "teacher" with specified options:

    ```javascript
    javascriptCopy codedb.createCollection("teacher", { capped: true, size: 10000000, max: 100, autoIndexId: false })
    ```


*   Create a regular collection named "courses":

    ```javascript
    javascriptCopy codedb.createCollection("courses")
    ```


*   Drop the "courses" collection:

    ```javascript
    javascriptCopy codedb.courses.drop()
    ```

Remember to keep your documentation up to date and organized for easy reference in the future.