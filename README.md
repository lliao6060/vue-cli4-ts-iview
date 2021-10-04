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


#### 使用webpack覆蓋樣式
  在vue中使用iview組件庫經常發現自己寫的樣式沒有生效，被iview覆蓋
  1. 我們要把樣式寫在scss中，並且去掉scoped。
  2. 加上多層div,防止出現覆蓋其他頁面樣式的問題。

```javascript
<style lang="scss">
  .test-wrapper {
    .test-inner {
      .ivu-card-body {
        padding: 15px;
      }
    }
  }
</style>
```

### 參考
- [配置](https://blog.csdn.net/u013843183/article/details/80455373)
- [css覆蓋](https://zeng-cy.blog.csdn.net/article/details/103169596?utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7Edefault-2.no_search_link&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7Edefault-2.no_search_link)
