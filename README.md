# vue cli4 + ts + iview

#### check
```
npm Ctrl+Shift+V
```

## install

1. first install 
  ```
  npm isntall iview --dave-dev
  ```
2. install `iview-loader`

```
npm install iview-loader --dave-dev
```

3. edit `vue.config.js`
```javescript=
module.exports = {
  module: {
    rules: [
      {
        test: /.js$/,
        loader: 'babel-loader',
        options: {
          presets: [
            ['@babel/preset-env', { targets: "defaults" }]
          ],
        }
      },
      {
        test: /.s?css$/,
        use: [
          CssExtractPlugin.loader, //抽取.vue檔裡的css變成獨立一隻檔案
          {
            loader: 'css-loader',
            options: {
              esModule: false,
              sourceMap: false,
            },
          },
          {
            loader: 'sass-loader',
            options: {
              sourceMap: false,
            },
          },
        ]
      },
      {
        test: /.vue$/,
        use: [
          {
            loader: 'vue-loader',
            options: {},
          },
          {
            loader: 'iview-loader',
            options: {
              prefix: false
              // false時可以使用<Row></Row>大寫標籤, 不須前贅詞
            },
          },
        ],
      },
      {
        test: /\.(png|jpe?g|gif|svg)(\?.*)?$/,
        loader: 'url-loader',
        options: {
          limit: 1000,
          outputPath: 'images',
        },
      },
    ]
  },
  devServer: {
    host: 'localhost'
  },
}
```

4. 在根目錄新增`declaration.d`
```javascript
declare module 'iview' {
  const iview: any;
  export default iview;
}
```

5.在`main.ts`
```javascript
import 'iview/dist/styles/iview.css'
import iview from 'iview'

Vue.use(iview)
```

就可以開心使用了

### 參考
See [here](https://blog.csdn.net/u013843183/article/details/80455373).
