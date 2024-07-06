# Nodejs

[Node.js Crash Course](https://www.youtube.com/watch?v=32M1al-Y6Ag&t)

```javascript title="nodejs"
import url from "url";

const urlString = "https://www.google.com/search?q=hello+world";

//URL Object
const urlObject = new URL(urlString);
console.log(urlObject.pathname);

//format()

console.log(url.format(urlObject));

//import.meta.url - file url
console.log(import.meta.url);

// fileURLToPath()
console.log(url.fileURLToPath(import.meta.url));

console.log(urlObject.search);

const params = new URLSearchParams(urlObject.search);
console.log(params);
console.log(params.get("q"));
params.append("limit", "5");
console.log(params);
params.delete("limit");
console.log(params);
```

```javascript title="nodejs"
console.log(process.argv);

// process.env
console.log(process.env);

//pid
console.log(process.pid);

// cwd
console.log(process.cwd());

// title
console.log(process.title);

// memoryUsage()
console.log(process.memoryUsage());

// uptime()
console.log(process.uptime());

process.on("exit", (code) => {
  console.log(`About to exit with code ${code}`);
});

// exit()
process.exit(0);
```

```javascript title="nodejs"
import path from "path";
import url from "url";

const filePath = "./dir1/dir2/test.txt";

// basename()
console.log(path.basename(filePath));

// dirname()
console.log(path.dirname(filePath));

// extname()
console.log(path.extname(filePath));

console.log(path.parse(filePath));

const __filename = url.fileURLToPath(import.meta.url);
const __dirname = path.dirname(__filename);
console.log(__filename, __dirname);

// join()
const filePath2 = path.join(__dirname, "dir1", "test.txt");
console.log(filePath2);

// resolve()
const filePath3 = path.resolve(__dirname, "dir1", "test.txt");
console.log(filePath2);
```

```javascript title="nodejs"
import os from "os";

// userInfo()
console.log(os.userInfo());

// totalmen()
console.log(os.totalmem());

// freemen()
console.log(os.freemem());

// cpus()
console.log(os.cpus());
```

```javascript title="nodejs"
// import fs from "fs";
import fs from "fs/promises";

// // readFile() -callback
// fs.readFile("./test.txt", "utf8", (err, data) => {
//   if (err) throw new Error();
//   console.log(data);
// });

// // readFileSync
// const data = fs.readFileSync("./test.txt", "utf8");
// console.log(data);

// // readFile() - Promise .then
// fs.readFile("./test.txt", "utf8")
//   .then((data) => {
//     console.log(data);
//   })
//   .catch((err) => console.log(err));

// readFile() - async/await
const readFile = async () => {
  try {
    const data = await fs.readFile("./test.txt", "utf8");
    console.log(data);
  } catch (error) {
    console.log(error);
  }
};

// writeFile()
const writeFile = async () => {
  try {
    await fs.writeFile("./test.txt", "Hello I am Yoad");
    console.log("file is writenn to..");
  } catch (error) {
    console.log(error);
  }
};

//appendFile
const appendFile = async () => {
  try {
    // await new Promise((resolve) => setTimeout(resolve, 1000));
    await fs.appendFile("./test.txt", "\nThis is appneded text");
    console.log("file appended..");
  } catch (error) {
    console.log(error);
  }
};

writeFile();
appendFile();
readFile();
```

```javascript title="nodejs"
import { EventEmitter } from "events";

const myEmitter = new EventEmitter();

function greetHandler(name) {
  console.log("Hello World" + name);
}

function goodbyeHandler(name) {
  console.log("Goodbye World" + name);
}

// Register event listeners
myEmitter.on("greet", greetHandler);
myEmitter.on("goodbye", goodbyeHandler);

//Emit events
myEmitter.emit("greet", "Jhon");
myEmitter.emit("goodbye", "Jhon");

// error handling
myEmitter.on("error", (err) => {
  console.log("An Error Ocured:", err);
});

//Simulate error
myEmitter.emit("error", new Error("Somthing went wrong"));
```

```javascript title="nodejs"
import crypto from "crypto";

// // createhash
// const hash = crypto.createHash("sha256");
// hash.update("password12345");
// console.log(hash.digest("hex"));

// // ramdomBytes
// crypto.randomBytes(16, (err, buf) => {
//   if (err) throw new Error();
//   console.log(buf.toString("hex"));
// });

// createCipheriv && createDecipheriv

const algotithm = "aes-256-cbc";
const key = crypto.randomBytes(32);
const iv = crypto.randomBytes(16);

const cipher = crypto.createCipheriv(algotithm, key, iv);
let encrypted = cipher.update(
  "Hello, this is a secret message",
  "utf-8",
  "hex"
);
encrypted += cipher.final("hex");
console.log(encrypted);

const decipher = crypto.createDecipheriv(algotithm, key, iv);
let decrypted = decipher.update(encrypted, "hex", "utf-8");
decrypted += decipher.final("utf-8");
console.log(decrypted);
```
