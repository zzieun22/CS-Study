# webpack

### 실행 

```
npm init -y
npm i webpack webpack-cli -D (--save-dev)
배포용 > 빌드할떄 빠지게 된다.
npm i lodash
```

lodash > dependency에 추가 되어있음 



### 스크립트로 설정하기 

```
"webpack --mode=none --entry=src/index.js --output-public/ouput.js"
```

이런식으로 옵션 줄 수 있다. 근데 넘길어 그래서 webpack.config.js 설정파일에 쓴다.



```js
// webpack.config.js
// `webpack` command will pick up this config setup by default
var path = require('path');
//노드 path 라이브러리
module.exports = {
  mode: 'none',
  entry: './src/index.js',
  output: {
    filename: 'main.js',
    path: path.resolve(__dirname, 'dist')
  }
};
```

------------------------

## webpack 설정

개발하면서 사용한 webpack.config.js 파일 설정 설명 

```
var path = require('path');
var HtmlWebpackPlugin = require('html-webpack-plugin');
var MiniCssExtractPlugin = require("mini-css-extract-plugin");
const { CleanWebpackPlugin } = require('clean-webpack-plugin')

module.exports = {
  mode: 'none',
  entry: {
      app: ['./src/js/index.js'],
   //   router: './src/router/router.js',
  },
   output: {
     filename: 'app.js', //app.js로 번들링
     path: path.resolve(__dirname, 'public'),
   },
  devServer: {
    publicPath: "/",
    port: 8080,
    overlay: true,
    hot: true,
  },
  module: {
    rules: [
          {
          test: /\.js$/,
          exclude: /node_modules/,
          use: {
              loader: 'babel-loader',
              options: {
                  presets: [['es2015', {modules: false}]],
                  plugins: [
                    'transform-async-to-generator',
                    'transform-class-properties',
                    'transform-regenerator',
                    'transform-runtime'
                  ]
                }
          }
      },
      {
          test: /\.css$/,
          use: [
            { loader: MiniCssExtractPlugin.loader },
            "css-loader"
          ],
      },
      {
          test: /\.html$/,
          use: 'html-loader'
      }
    ]
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: './src/index.html',
      filename: 'index.html',
    }),
    new MiniCssExtractPlugin({ filename: 'style.css' }),
    new CleanWebpackPlugin({
        cleanAfterEveryBuildPatterns: ['dist']
      })
  ],
  devtool: 'source-map'
};
```

package.json > scripts 

```
    "test": "jest --env=jsdom",
    "build": "webpack --mode=production --output public/app.js",
    "build-dev": "webpack --mode=development",
    "start": "webpack-dev-server --hot" 
```



```
"start": "webpack-dev-server --hot  /////핫로딩 
```

```
 devServer: {
    publicPath: "/",
    port: 8080,
    overlay: true,
    hot: true, /////핫로딩 
  },
```

위 두개는 똑같이 실행된다.

```
"build": "webpack --mode=production --output public/app.js",
```

```
 output: {
     filename: 'app.js', //app.js로 번들링
     path: path.resolve(__dirname, 'public'),
   },
```

위 두개도 똑같이 실행된다.



### mode

production / development / none이있음 

production : 배포

### entry

빌드할 대상

웹 자원을 변환하기위해 필요한 것들 (진입점)

```
  entry: {
      app: ['./src/js/index.js'],
  },
```

저런식으로`[./src/js/index.js']` 한개만 추가하던지 

`['./src/js/index.js' , './src/js/router.js' ]`  이렇게 여러개 추가 할 수 있음 

### output 

웹팩으로 돌리고난 결과물의 파일 경로 

```
filename : 
path : 유효한 파일 경로 넣으면됨
```

```
module.exports = {
  output: {
    filename: '[chunkhash].bundle.js' //고유 값을 붙여주게 된다. 브라우저캐싱때문에 강제 새로고침 캐시 비워져야해서 chunkhash같은 고유값을 넣어줄 수 있다.
  }
};
```



```
   output: {
     filename: 'app.js', //app.js로 번들링
     path: path.resolve(__dirname, 'public'),
   },
```

이렇게 쓰면 

![image](https://user-images.githubusercontent.com/36434665/125899604-1794105d-fd46-4a07-a88a-6fff2eb649f3.png)

이렇게 public/밑에 app.js 로 내가 원하는파일이 모두 번들링되어 나온다. 

### module

#### rules  

규칙

#### Loader 

웹팩자원들로 변환 할 수 있도록 도와주는 속성 

**css관련**

```js
'style-loader', //wepack안에들어간 스타일을 웹팩안에 넣어주는 것 
'css-loader' //css가 들어갈 수 있게 한것 
```

```
'style-loader', 'css-loader' // 오른쪽에서 왼쪽 순으로 로드 된다. 
```

```js
var path = require('path');

module.exports = {
  mode: 'none',
  entry: './index.js',
  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'dist')
  },
  module: {
    rules: [
      {
        test: /\.css$/,
        use: ['style-loader', 'css-loader']
      }
    ]
  },
}
```

#### plugins

ex>

```js
// webpack.config.js
var path = require('path');
var MiniCssExtractPlugin = require("mini-css-extract-plugin");

module.exports = {
  mode: 'none',
  entry: './index.js',
  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'dist')
  },
  module: {
    rules: [
      {
        test: /\.css$/,
        use: [
          { loader: MiniCssExtractPlugin.loader },
          "css-loader"
        ]
      }
    ]
  },
  plugins: [
    new MiniCssExtractPlugin()
  ],
}

```

style-loader 를 분리했음 

index.html에서 

```
  <link rel="stylesheet" href="./dist/main.css">
```

를 추가해줘야한다. 



plugin은 결과물에 대한 정보를 바꾼다. 

dist폴더에 bundle.js/ main.css를 따로 떨어뜨릴수있음 



**추가적인 기능을 제공하는 속성이다.** 

배열에는 생성자함수로 생성한 객체 인스턴스만 추가될 수 있음 



### source map

```
devtool: 'source-map'
```

  추가하면 console.log입력시 기존 폴더파일이 위치한 곳을 보여준다.(웹팩으로 말아진 파일 말고 기존 파일 그대로)



**npm run build** 는 webpack명령어가 실행되면서 고유 해시값이 붙는다 



## 웹팩 데브 서버

웹앱을 개발하는 과정에서 유용하게 쓰인다. 

```
npm i webpack webpack-cli webpack-dev-server html-webpack-plugin -D
```

