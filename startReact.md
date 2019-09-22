## INICIANDO UM PROJETO COM REACT

**1. Iniciar o projeto com:**

```
yarn init -y
```

**2. Para garantir que o Prettier não coloque aspas duplas em torno das strings, o que contraria o padrão Airbnb que exige aspas simples, cria-se o arquivo .prettierrc na pasta raiz com as diretivas:**

```
{
  "singleQuote": true,
  "trailingComma": "es5"
}
```

**3. Instalando a extensão EditorConfig | [Documentação](https://github.com/editorconfig/editorconfig-vscode) no VS Code. Após a instalação clique com o botão direito no diretório raiz e escolha a opção Generate .editorconfig**

_No arquivo .editorconfig gerado, certifique-se que ele esteja com as seguintes informações:_

```
root = true

[*]
indent_style = space
indent_size = 2
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true
```

# Bibliotecas a serem instaladas inicialmente para um projeto utilizando React:

**Bibliotecas do Babel e Webpack**

```
yarn add @babel/core @babel/preset-env @babel/preset-react webpack webpack-cli -D
```

**Bibliotecas do react e react-dom**

```
yarn add react react-dom
```

**Biblioteca do babel-loader**

```
yarn add babel-loader -D
```

**Biblioteca para atualizar o HTML toda vez que tiver uma alteração**

```
yarn add webpack-dev-server -D
```

**Bibliotecas do style-loader e css-loader**

```
yarn add style-loader css-loader -D
```

**Biblioteca para um loader de imagem**

```
yarn add file-loader -D
```

**Biblioteca para utilizar o state**

```
yarn add @babel/plugin-proposal-class-properties -D
```

**Biblioteca para validar os propTypes no React**

```
yarn add prop-types
```

# Após a instalações das bibliotecas, precisamos configurar os arquivos do babel, webpack e package.json

**babel.config.js**

```js
module.exports = {
  presets: ['@babel/preset-env', '@babel/preset-react'],
  plugins: ['@babel/plugin-proposal-class-properties'],
};
```

**webpack.config.js**

```js
const path = require('path');

module.exports = {
  entry: path.resolve(__dirname, 'src', 'index.js'),
  output: {
    path: path.resolve(__dirname, 'public'),
    filename: 'bundle.js',
  },
  devServer: {
    contentBase: path.resolve(__dirname, 'public'),
  },
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: {
          loader: 'babel-loader',
        },
      },
      {
        test: /\.css$/,
        use: [{ loader: 'style-loader' }, { loader: 'css-loader' }],
      },
      {
        test: /.*\.(gif|png|jpe?g)$/i,
        use: {
          loader: 'file-loader',
        },
      },
    ],
  },
};
```

# Criar duas pasta na raíz do projeto

**-> public**

**-> src** - _Dentro da pasta src, vamos sempre criar um arquivo **index.js**, que é o arquivo de entrada da nossa aplicação, tudo vai partir desse arquivo_

**\*Exemplo**:

```js
const soma = (a, b) => a + b;

alert(soma(1, 3));
```

**Alterar o package.json para incluir os scripts**

```js
 "scripts": {
    "build": "webpack --mode production",
    "dev": "webpack-dev-server --mode development"
  },
```

- **Produção** - _build_
- **Desenvolvimento** - _dev_

**Executar o comando abaixo para gerar o arquivo bundle.js**

```js
yarn dev
```

**Quando criar o arquivo index.html, precisamos alterar o arquivo webpack.config para incluir o caminho para encontrar onde está o arquivo _index.html_**

```js
devServer: {
    contentBase: path.resolve(__dirname, 'public'),
  },
```

**Na pasta /src, precisamos criar os arquivos _App.js_ e _App.css_**

**No arqbuivo _index.html_ precisamos sempre passar no _body_ essa estrutura:**

```js
<body>
  <div id="app"></div>
  <script src="./bundle.js"></script>
</body>
```

**O arquivo _App.js_ é onde vamos passar todos os componentes que serão executados no arquivo _index.html_**

**Estrutura do arquivo _index.js_**

```js
import React from 'react';
import { render } from 'react-dom';

import App from './App';

render(<App />, document.getElementById('app'));
```

**Estrutura do arquivo _App.js_**

```js
import React from 'react';
import './App.css';

import Header from './components/Header';
import PostList from './components/PostList';

function App() {
  return (
    <>
      <Header />
    </>
  );
}

export default App;
```
