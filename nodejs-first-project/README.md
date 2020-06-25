Primeira API feita com base no curso da Rocket.

Documentação para estudos:

Instalação NodeJS no Mint:

https://github.com/nodesource/distributions/blob/master/README.md

Comandos:
curl -sL https://deb.nodesource.com/setup_13.x | sudo -E bash -
sudo apt-get install -y nodejs

Instalação do Yarn:
 curl -o- -L https://yarnpkg.com/install.sh | bash


Instalação do Docker:
 sudo apt-get install  apt-transport-https ca-certificates curl gnupg-agent software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo apt-key fingerprint 0EBFCD88
 sudo add-apt-repository  "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"
 sudo apt-get update
 sudo apt-get install docker-ce docker-ce-cli containerd.io
 sudo docker run hello-world


Instalando a image do mongo com docker:
 sudo docker pull mongo
 sudo docker run --name mongodb -p 27017:27017 -d mongo
 

*Software Robo3T para poder interagir com o banco.

















Iniciando projeto com NodeJS

Dentro da pasta do projeto:
npm init -y

Estrutura:
*Todos os arquivos do projeto dentro de uma pasta chamada “src”.
Pasta banco /src/database/index.js

Módulo para atualizar automaticamente o server, adicionando apenas como dependência de desenvolvedor:
npm install -D nodemon

Para ativá lo necessita adicionar esta linha na parte de scripts no package.json e depois em um terminal o comando posterior:
"dev": "nodemon server.js"
npm run dev

Para importar os módulos usa-se a seguinte sintaxe:
const express = require('express');

Para iniciar o CORE da aplicação:
const app = express();

Identificando que estamos usando os módulos, abaixo para entender JSON:
app.use(bodyParser.json());

Entender parâmetros via URL:
app.use(bodyParser.urlencoded({ extend: false }));

Indicando a porta do app:
app.listen(3001);

Sistema para rotas e requests NodeJS (Express):
yarn add express

Sistema para que o NodeJS entenda informações em JSON e  parâmetros na URL:
yarn add body-parser

Sistema para conectar com banco de dados mongo-db:
yarn add mongoose

Declarar o módulo do mongoose no arquivo de banco:
const mongoose = require('mongoose');

Primeira rota na raiz, toda rota tem parâmetros “req” e “res”. O req são os dados da requisição, o res é o objeto uma resposta ao usuário:
app.get('/', (req, res) => {
  res.send('OK');
});

Módulo para permissão de acesso da API para diferentes hosts:
const cors = require('cors');
app.use(cors());

Exemplo de models, sempre criar dentro de /src/models/NomeModel.js:
const mongoose = require('../database');
 
const UserSchema = new mongoose.Schema({
   name: {
       type: String,
       required: true,
   },
   email: {
       type: String,
       unique: true,
       required: true,
       lowercase: true,
   },
   password: {
       type: String,
       required: true,
       select: false,
   },
   createdAt: {
       type: Date,
       default: Date.now,
   },
});
const User = mongoose.model('User', UserSchema);
module.exports = User;


Módulo para automatizar os requires de models dentro do server.js:
yarn add require-dir
const requireDir = require('require-dir');
requireDir('./src/models');


Módulo para encriptação de senha:
yarn add bcryptjs
const bcrypt = require('bcryptjs');
 





