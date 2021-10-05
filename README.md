# .bashrc
```
source ~/.bash_alias
source ~/.bash_functions
```

# Alaises
```alias start_mongo='brew services start mongodb-community@4.2'
alias stop_mongo='brew services stop mongodb-community@4.2'
alias caruby='rvm use ruby-2.4.6'
alias rails_edit='EDITOR="code --wait" rails credentials:edit'
alias start_pg='brew services start postgresql'
alias stop_pg='brew services stop postgresql'
```

# functions 
```function mkcd () {
  mkdir $1
  cd $1 
} 

function mkrepo () {
  mkdir $1
  cd $1
  git init 
  touch README.md
  echo "# "$1 > README.md
  git add . 
  git commit -m "Initialized repo" 
} 

function plzignore () {
    git rm --cached $1
    echo $1 >> .gitignore
}

function genSRI () {
  HASH=$(cat $1 | openssl dgst -$2 -binary | openssl base64 -A)
  if [[ $1 =~ ^.*\.css$ ]]; then
   echo "Hashed link tag copied to clipboard"
   echo "<link integrity=\"${2}-${HASH}\" rel=\"stylesheet\" href=\"./${1}\">" | pbcopy
  elif [[ $1 =~ ^.*\.js$ ]]; then
    echo "Hashed script tag copied to clipboard"
    echo "<script src=\"./${1}\" integrity=\"${2}-${HASH}\"><\script>" | pbcopy
  else 
   echo "Wrong file type"
  fi  
}

 function mktouch() {
    if [ $# -lt 1 ]; then
        echo "Missing argument";
        return 1;
    fi
    for f in "$@"; do
        mkdir -p -- "$(dirname -- "$f")"
        touch -- "$f"
    done
}
function cra() {
  npx create-react-app "$@"
  cd $1
}
```