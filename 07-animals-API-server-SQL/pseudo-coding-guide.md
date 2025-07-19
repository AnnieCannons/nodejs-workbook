# 🚧 Express API Pseudo-Coding Guide
## Follow this guide to help you pseudo-code your API Endpoints! 

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

**Example:**
```js
async function yourHelperFunction(parameter) {
  // Write your SQL query here
  const result = await db.query("SQL QUERY", [values]);

  // Return result if needed
  return result.rows;
}
```

---

### ✨ 5. Will the helper function return anything?

Choose one:
- ✅ Yes → it returns data from the database (like a SELECT query)
- ❌ No → it just performs an action (like INSERT or DELETE)

---

### ✨ 6. What SQL query will it use?

Write your SQL query using `$1`, `$2`, etc. for dynamic values.

**Example:**
```sql
SELECT * FROM animals WHERE name = $1
```

---

### ✨ 7. What response will the API send?
Choose one:
- `res.json(data);` → use if you're sending an object or array
- `res.send("Success!");` → use if you're sending a plain status message

---

## 💡 Example Implementation — GET Endpoint

### 🔁 API Endpoint
```js
app.get("/get-one-animal/:name", async (req, res) => {
  const animalName = req.params.name;
  const animal = await getOneAnimal(animalName);
  res.json(animal);
});

```

### 🛠️ Helper Function
```js
async function getOneAnimal(animalName) {
  const result = await db.query("SELECT * FROM animals WHERE name = $1", [
    animalName,
  ]);
  return result.rows[0];
}

```

---

##

### 🔁 API Endpoint
```js
app.post("/add-one-animal", async (req, res) => {
  const newAnimal = req.body;
  addOneAnimal(newAnimal);
  res.send("The animal was successfully added!");
});

```

### 🛠️ Helper Function
```js
async function addOneAnimal(animal) {
  await db.query(
    "INSERT INTO animals (name, category, can_fly, lives_in) VALUES ($1, $2, $3, $4)",
    [animal.name, animal.category, animal.can_fly, animal.lives_in]
  );
}

```
