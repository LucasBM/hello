# =========================

# 1) CRIAR PROJETO + GITHUB

# =========================

mkdir hello
cd hello

npm init -y

echo "module.exports = () => 'Hello world';" > index.js

git init
git add .
git commit -m "feat: initial commit"

git branch -M main
git remote add origin https://github.com/LucasBM/hello.git
git push -u origin main

# =========================

# 2) PUBLICAR NO NPM

# =========================

npm login
npm publish --access public

# =========================

# 3) TESTAR EM OUTRA PASTA

# =========================

cd ..

mkdir teste-lib
cd teste-lib

npm init -y
npm install @lucasbertoloto/hello

node -e "console.log(require('@lucasbertoloto/hello')())"

# =========================

# 4) ALTERAR PROJETO

# =========================

cd ../hello

echo "module.exports = () => 'Hello world v2';" > index.js

git add .
git commit -m "feat: update message"
git push

# =========================================================

# 4.2) VERSIONAMENTO (ESCOLHA UMA DAS OPÇÕES)

# =========================================================

# -------- OPÇÃO A: TAG MANUAL --------

# (edite o package.json e mude a versão antes, ex: 0.1.1)

git add package.json
git commit -m "chore: bump version to 0.1.1"

git tag -a v0.1.1 -m "Release v0.1.1"

git push
git push --tags

# -------- OPÇÃO B: AUTOMÁTICO (RECOMENDADO) --------

npm version patch (major, minor, patch)

git push
git push --tags

# =========================

# 4.3) PUBLICAR NOVA VERSÃO

# =========================

npm publish --access public

# =========================

# 5) TESTAR NOVA VERSÃO

# =========================

cd ../teste-lib

npm install @lucasbertoloto/hello@latest

node -e "console.log(require('@lucasbertoloto/hello')())"
