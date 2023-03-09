# Server set-up procedure

## initial software install

In the directory you want to use to hold the server files run:

### npm package manager

```terminal
npm init -y
```

adds the package.json file. the node_modules folder and package-lock.json are added when a dependancy is installed

## Dependancies

### express

http://expressjs.com/

```terminal
npm i express
```

### dotenv

https://www.npmjs.com/package/dotenv

```terminal
npm install dotenv
```

### node-postgres

https://www.npmjs.com/package/pg

```terminal
npm install pg
```

### node-pg-format

https://www.npmjs.com/package/node-pg-format

```terminal
npm install node-pg-format
```

## devDependancies

should be installed with the -D flag

### jest

https://jestjs.io/

```terminal
npm install -D jest
```

### supertest

https://www.npmjs.com/package/supertest

```terminal
npm install -D supertest
```

## folder and file structure

app.js is the main file, but the code is abstracted into other files in line with the Model-View-Controller methology (MVC)