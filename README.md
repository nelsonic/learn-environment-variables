# Learn Environment Variables [![Join the chat at https://gitter.im/dwyl/chat](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/dwyl/chat/?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

Learn how to use Environment Variables keep your secret keys safe & secure!

![rainforest environment](http://i.imgur.com/aL1qD74.jpg)
<sup>*random picture of a rainforest river ... environment ... get it? ... tenuous connection? I liked it! hope you do too!* </sup>


## *Why*?

If you put an API key on GitHub it means out of your control and someone
(*unauthorised*) has access ...  
the physical-world equivalent is writing your home address on the keyring
for your house keys and  
then losing your keys in a bad neighborhood, you'll be *lucky* if nobody uses
your keys to  
"borrow" the TV from your house...!

Avoid (*accidentally*) committing (*exposing*) your ***private keys***, ***passwords*** or other ***sensitive details***  
(*by hard-coding in them in your script*) to GitHub by storing them
as environment variables.

## *What*?

If you are new to "***back end***" development, you may not have encountered
environment variables
before, this quick guide will tell you *all* you need to know!

[The Twelve-Factor App](http://12factor.net/config) ***best practice***
recommends storing your app's configuration
in the "*environment*", but what does that mean?

> This *simply* means that you save any configuration both the values that are the  
same everywhere you run your app and the keys that change depending on where  
you are running the app, in the environment where you are running your app.

## *How*?

### List all the *Default* Environment Variables

In your terminal type: `printenv` and tap the `enter` key.

You should see something like this:
```js
{
  TERM_PROGRAM: 'Apple_Terminal',
  SHELL: '/bin/bash',
  TERM: 'xterm-256color',
  TERM_PROGRAM_VERSION: '343.7',
  USER: 'n',
  PWD: '/Users/n/code/learn-environment-variables',
  LANG: 'en_GB.UTF-8',
  _system_arch: 'x86_64',
  _system_name: 'OSX',
  _: '/usr/local/bin/node'
}
```
This is a list of all the variables defined in your environment,
in this case we are running `printenv` on a Mac using the "Terminal" app,  
if you are on Linux/Unix using Bash/etc.
you will see something slightly different.

#### Log the list of environment variables available to node.js in `process.env`

Node.js gives you access to the variables defined in your environment
in the `process.env` ***global object***.

Create a file called `printenv.js` and type/paste the following line in it:
```js
console.log(process.env);
```
Run this script in your terminal:
```sh
node printenv.js
```

### Adding Variables to your Environment

There are 3 ways to add variables to the environment where your app is running.

#### 1. Command-Line Arguments

When you run your node program/app you can include settings as environment variables
for example, try running the following:

```sh
PORT=1337 node printenv.js
```
Notice how the PORT variable is the *first element* displayed in the console?
You are now able to access the `PORT` value in your node.js script
by reference: `process.env.PORT`

including your config in the command you use to run your script/app gets
cumursome when you have lots of API Keys or Databases ...

#### 2. Export the Variable to your Environment

An improvement on this command-line arguments is to export the variable
in your terminal:

Type/paste this in your terminal window and tap enter:
```sh
export HELLO=WORLD
```
Now `printenv` or `node printenv.js` to see it printed!
the `HELLO` key is now available in the `process.env` object
try adding the following line to your `printenv.js` file:

```js
console.log(">> Hello", process.env.HELLO);
```
Now run it in your terminal:
```sh
node printenv.js
```
What do you see?

```sh
>> Hello WORLD
```

Exporting your keys to your environment using `export MY_VAR=HAI` works
but if you use a terminal that does not *save* your variables across sessions,
(e.g. if you close your terminal window!) you will have to keep exporting them!

Thankfully there's a 3rd (*easier*) way!

#### 3. Use a `config.env` file *locally* which you can `.gitignore`

The way we prefer to manage our Environment Variables on our development machines
is using a `config.env` file which gets loaded into our app *once* and
adds any entries in the `.env` file to the `process.env` (*global object*).

We wrote the **env2** ***node.js module*** to load configuration from a `.env` or
`.json` file.

Loading your environment variables from a `config.env` file is as easy as "ABC"!

##### A. Create your `config.env` file

Create a `config.env` file in the root of your project and insert
your key/value pairs in the following format of `KEY=VALUE`:

```sh
DB_HOST=127.0.0.1
DB_PORT=9200
DB_USER=TheSpecial
DB_PASS=EverythingIsAwesome
```

##### B. Install `env2` and save it to your `package.json`

Install the **env2** module from NPM and save it as a Dependency in your
`package.json` file:

```sh
npm install env2 --save
```

##### C. Invoke `env2` and use the variable in your script

Loading your configuration is a 1-line call to node.js's `require` method
which loads **env2** and invokes it with your `config.env` file as the argument:

```js
require('env2')('config.env');    // loads all entries into process.env

console.log(process.env.DB_HOST); // "127.0.0.1"
```

Now you can access any of the entries in your `config.env` file as a key
in the `process.env` Object e.g: `process.env.PORT` is `9200` (in our example above).


##### D. Add `config.env` to your `.gitignore` file!

```sh
echo config.env >> .gitignore
```

This ensures that the `config.env` is not "tracked" in .git and thus
will not be public on GitHub. i.e only visible on your local machine.  
If you are new/rusty on using `.gitignore` file to omit files/folders
from your Git/GitHub repo read: http://git-scm.com/docs/gitignore

<sup>1</sup>**env2** solves the problem of loading config files,
we *recommend* using **env2** because the ***code is clean, tested & documented***,
but there are *other* solutions to this problem on NPM you can chose from
depending on your needs. But if **env2** does cover your *specific* use-case,
please tell us about it, we *always* love helping to solve problems and
enhance our modules to be more useful to people! [![Join the chat at https://gitter.im/dwyl/chat](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/dwyl/chat/?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)



## Research & Background Reading

+ Detailed article: https://en.wikipedia.org/wiki/Environment_variable
+ The Twelve-Factor App > Configuration: http://12factor.net/config
+ Env vars on Arch Linux: https://wiki.archlinux.org/index.php/Environment_variables

# Thanks!

Thanks for learning about Environment Variables with us!  
If you have any questions, please ***ask***!! [![Join the chat at https://gitter.im/dwyl/chat](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/dwyl/chat/?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)  
Please :star: this repo to help spread the word!
