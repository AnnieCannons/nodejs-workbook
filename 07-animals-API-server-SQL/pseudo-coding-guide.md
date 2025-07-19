# 🚧 Express API Pseudo-Coding Guide
## Follow this guide to help you pseudo-code your API Endpoints! 

You'll start by writing the API endpoint first, then its helper function second. 

---

## Writing the API Endpoint

---

### ✨ 1. What kind of request is this?

Choose one: `GET`, `POST`

**Example:**

```js
app.get("/your-endpoint", async (req, res) => { ... });
app.post("/your-endpoint", async (req, res) => { ... });
```



---

### ✨ 2. What is the API endpoint URL?

**Example:**
- `/get-all-animals`
- `/get-one-animal/:name`
- `/add-one-animal`

---

### ✨ 3. Will you need to get any data from the request, such as a request body or dynamic parameter?
If yes, how will you access the data?

**Examples:**

```js
// If using a dynamic route parameter:
const name = req.params.name;

// If receiving data from the request body:
const animal = req.body.animal;
```

---

### ✨ 4. Will you need a helper function?
If yes, describe what it should do and give it a **verb/action-based name.**

**Examples:**
```js
getOneAnimal(animalName);
getAllAnimals();
addOneAnimal();
updateOneAnimal();
```

---

### ✨ 5. Will the helper function return anything?

Choose one:
- ✅ Yes → if it returns data from the database (like a SELECT query), save its return value in a variable
- ❌ No → it just performs an action (like INSERT or DELETE), so you don't need to save a return value

Example:
```js
// these helper functions return data from the database, so we save its return value in a variable 
const animal = await getOneAnimal(animalName);
const animals = await getAllAnimals()

// these helper functions perform an action on the database, but don't need to return any data  
addOneAnimal();
deleteOneAnimal();
updateOneAnimal();
```

---

### ✨ 6. What response will the API send?
Choose one:
- `res.json(data);` → use if you're sending an object or array
- `res.send("Success!");` → use if you're sending a plain status message

---

## 💡 Example Implementation — API Endpoints

```js
app.get("/get-all-animals", async (req, res) => {        // declaring our GET API endpoint
  const animals = await getAllAnimals();                 // calling the helper function, and saving the data we get back in a variable
  res.json(animals);                                     // sending the data back in the response
});
```
```js
app.get("/get-one-animal/:name", async (req, res) => {  // declaring our GET API endpoint
  const animalName = req.params.name;                   // getting the user-inputted value from the request params
  const animal = await getOneAnimal(animalName);        // calling the helper function, and saving the data we get back in a variable
  res.json(animal);                                     // sending the data back in the response
});
```
```js
app.post("/add-one-animal", async (req, res) => {       // declaring our POST API endpoint
  const newAnimal = req.body;                           // getting the data passed in through the request body
  addOneAnimal(newAnimal);                              // calling the helper function, which performs an action on the database 
  res.send("The animal was successfully added!");       // sending a status message in the response
});
```

---

## Writing the Helper Function

---

### ✨ 1. What is the helper function called? Should it accept a parameter? 

For example, if we want our helper function to get a certain animal based on its name, we need to pass that name in as a parameter. 

**Example:**
```js
async function getOneAnimal(animalName) {
  
}
```

---

### ✨ 2. What SQL query will it use?

Write your SQL query using `$1`, `$2`, etc. for dynamic values.

**Example:**
```js
const result = await db.query("SELECT * FROM animals WHERE name = $1", [animalName]);
await db.query(
    "INSERT INTO animals (name, category, can_fly, lives_in) VALUES ($1, $2, $3, $4)",
    [animal.name, animal.category, animal.can_fly, animal.lives_in]
  );
}
```

---

### ✨ 3. Will the helper function return anything?

Choose one:
- ✅ Yes → it returns data from the database (like a SELECT query) using `result.rows` 
- ❌ No → it just performs an action (like INSERT or DELETE)

---

## 💡 Example Implementation — Helper Functions

```js
async function getAllAnimals() {
  const result = await db.query("SELECT * FROM animals");
  return result.rows;
}
```
```js
async function getOneAnimal(animalName) {
  const result = await db.query("SELECT * FROM animals WHERE name = $1", [
    animalName,
  ]);
  return result.rows[0];
}
```
```js
async function addOneAnimal(animal) {

  // querying the database and adding the animal
  await db.query(
    "INSERT INTO animals (name, category, can_fly, lives_in) VALUES ($1, $2, $3, $4)",
    [animal.name, animal.category, animal.can_fly, animal.lives_in]
  );
}
```
