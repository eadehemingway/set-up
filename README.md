# Set up like a pro

## 1. Adding a SSH key to github

### whats the problem?

you will not have the right access rights to private git repositories if you have not set up your SSH key. If you try and clone a private repo it will not allow you to do so.

### Whats the solution ?

You need to create a connection between your laptop and your github account. An SSH key has a private key and a public key, the private one lives in a folder on your laptop and you add the public one to whichever places you want to recognise your laptop (in this case github). 

run this command in your terminal: 

```jsx
ls ~/.ssh
```

This is saying "list all the files you have in your `.ssh` folder". If it says something like "that folder doesnt exist" then you dont have one and you will need to create one. If you do have one you should see a `id_rsa.pub` file which is where the public half of the key lives (and you dont need to generate another one. 

To generate a SSH key run this command:

```jsx
ssh-keygen
```

which will ask you a bunch of questions and you just press enter for all of them. This will create an SSH key with all the default values. if you run `ls ~/.ssh` now you should see it exists and includes a `id_rsa.pub` file. 

Now we need to copy the public key by running: 

```jsx
pbcopy < ~/.ssh/id_rsa.pub
```


This copies the ssh key to your clipboard. 

Now go to github settings and look for `SSH and GPG keys` and click `New SSH key`. Paste your public key in the box and give it a name that relates to your laptop. Save it and you are good to go!

### How to check its worked?

Clone a repo (making sure you select the SSH tab and not the HTTPS - see photo below) and you should have no issues.
<img width="389" alt="Screenshot 2021-09-30 at 16 58 17" src="https://user-images.githubusercontent.com/32163243/135479954-1df2c0f5-d189-4439-9c80-532e971ede62.png">

## 2. ESLint format on save

### whats the problem?

There are lots of tiny things that Eslint will complain about if it is not done the right way e.g. it will complain if there is unnecessary trailing whitespace or if we used single quotes instead of double quotes. It is a complete waste of time to fix these manually. 

### whats the solution?

Set vscode up so that Eslint fixes on save, i.e. it fixes its own issues every time you press save. 

- Firstly make sure you have eslint installed globally: `npm i eslint -g`
- Then create a `.eslintrc.js` file with this in it (this is a very basic eslint file, see other readme for more complex projects)
    ```
    module.exports = {
        "parserOptions": {
            "ecmaVersion": 2017
        },
        "env": {
            "es6": true
        },
        "rules": {
            "indent": ["error", 4],
            "semi": ["error", "always"],
            "quotes": ["error", "double"]
        }
    };
    ```

- Go to your Vscode settings  (`cmd` + `,`), then click the icon in the top right corner that looks like this: <img width="51" alt="Screenshot 2021-09-30 at 16 56 07" src="https://user-images.githubusercontent.com/32163243/135479605-931f48e2-d742-455d-b2e7-bb5cac1b331e.png"> This will take you to the json version of your settings, copy and paste in this block: 

    ```js
    // These are all my auto-save configs
    "editor.formatOnSave": true,
    // turn it off for JS and JSX, we will do this via eslint
    "[javascript]": {
      "editor.formatOnSave": false
    },
    "[javascriptreact]": {
      "editor.formatOnSave": false
    },
    // tell the ESLint plugin to run on save
    "editor.codeActionsOnSave": {
      "source.fixAll": true
    }
    ```
- Finally go to Vscode extentions and install the 'ESLint' extention.

### How to check its worked?

Remove a semicolon in a js file, press save and it should add it back for you. 

## 3. Add Console wrap to make console.log into a keyboard shortcut

### whats the problem?

We developers console.log all the time, and it wastes time having to type it out manually every time

### Whats the solution ?

Go to VSCode extentions and add "Wrap Console Log". Then go to your keyboard shortcuts and search for `wrap down prefix console log` and double click to change the shortcut. Change to command + L 

### How to check its worked?

Go to a file in VSCode, put your cursor on a variable and press command + L, you should see a console.log appear on the line below with the prefix of the variable name.

## 4. Use oh my zsh in your terminal to have a better terminal experience

### whats the problem?

The standard terminal is hard to read, it doesnt tell you which folder you are in or what branch you are on, so you waste checking these things.

### Whats the solution ?

Add `oh my zsh` ([https://ohmyz.sh/](https://ohmyz.sh/)) to your terminal by running this command:


```jsx
$ sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" = code -w
```

### How to check its worked?

If you go into a git repository it should have what branch you are on in brackets before the end of the prompt line. You can add different color themes easily just have a look at the documentation if interested [https://github.com/ohmyzsh/ohmyzsh/wiki](https://github.com/ohmyzsh/ohmyzsh/wiki)

## 4. Set default editor to VScode so that nothing opens in vim ever again

### whats the problem?

open up a repo, add a change and write `git commit` without a message. Git will need you to write a commit message, so it opens a vim console. Vim is tedious and hard to use

### Whats the solution ?

run this command in your terminal, it adds `code.editor = code -w` to your clobal git config file

```jsx
git config --global core.editor "code -w"
```

### How to check its worked?

open up a repo, add a change and write `git commit` without a message. Git will need you to write a commit message, but this time it will open the file in vscode!

## 5. Add git lens for easier interactive rebase

### whats the problem?

Rebasing can be confusing and it is easy to get confused about which commit would get squashed onto which commit (the one above it or below it), and moving commits around in a text editor is not as easy as it could be. To see what I mean you need to start an interactive rebase in a test branch with at least one test commit on it, run this command to start the rebase:

```jsx
git rebase -i master
```

Git will open the commits either in Vim or Vs code depending on your default editor. Try rearranging the order of commits.

### Whats the solution ?

go to VSCode extensions and install 'GitLens'

### How to check its worked?

run the rebase again and this time you should see a lovely Gitlens ui that allows you to drag and drop commits into whatever order you wish and gives other useful visual aids such as showing which commit a squashed commit would get squashed into.
