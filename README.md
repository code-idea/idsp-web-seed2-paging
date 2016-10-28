# idsp-web-seed2-paging
分页组件

安装方法

### 1. 下载程序包
```bash
npm i idsp-web-seed2-paging --save
```

### 2. 配置文件依赖

找到 `index.html` 文件的systemjs配置,加入 `idsp-web-seed2-paging`  配置
```js
SystemJS.config({
    transpiler: 'ts',
    typescriptOptions: {
        // ...
    },
    packages: {
        //...
        lesscss: {main: './dist/less.min.js'},
        css: {main: 'css.js'},
        less: {main: 'less.js'},
       
        // 组件设置 
        'idsp-web-seed2-paging': {main: 'paging.ts'},
    
        "src": {
            //...
        }
    },
    meta: {
        '*.less': {loader: 'less'},
        '*.css': {loader: 'css'},
        // ...
    },
    
    map: {
        css: 'node_modules/systemjs-plugin-css',
        less: 'node_modules/systemjs-plugin-less',
        lesscss: 'node_modules/less',
        // ...
        'idsp-web-seed2-paging': 'node_modules/idsp-web-seed2-paging',
    }
});
```

### 3. 在项目`src/common/directives/directives.ts`中依赖组件

```ts
//...
import paging from "idsp-web-seed2-paging";

export const mod = module('directives', [...others, paging]);
```


### 4. 接下来就可以使用分页了
```html
<paging option="testOption"></paging>
```
```ts
@Route({
  ...
  controllerAs : 'Ctrl'
})
@Controller
exports class PageCtrl{
  public pagingOption:PagingOption = {
     params : {}
  };
  
  constructor(TestServer){
    this.pagingOption.resource = TestServer;
  }
}
```

#### 指令属性参数

<table>
  <thead>
    <tr>
      <th>参数</th>
      <th>类型</th>
      <th>描述</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>option</td>
      <td>PagingOption</td>
      <td>用来配置设置分页组件</td>
    </tr>
  </tbody>
</table>

#### PagingOption 参数
<table>
  <thead>
    <tr>
      <th>参数</th>
      <th>类型</th>
      <th>描述</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>resource</td>
      <td>后台Server接口</td>
      <td>发送分页请求的Server接口</td>
    </tr>
    <tr>
      <td>method (可选)</td>
      <td>String</td>
      <td>请求类型，默认 `get`</td>
    </tr>
    <tr>
      <td>limit (可选)</td>
      <td>Number</td>
      <td>请求数据大小，默认10条</td>
    </tr>
    <tr>
      <td>limitList (可选)</td>
      <td>Number[]</td>
      <td>配置分页器页数选择下拉框中，默认 [10,20,30,40,50]</td>
    </tr>
    <tr>
      <td>resultList</td>
      <td>Array</td>
      <td>服务器返回的数据</td>
    </tr>
    <tr>
      <td>format (可选)</td>
      <td>format(list:any[])=>any</td>
      <td>服务器返回数据后格式化函数，默认无</td>
    </tr>
    <tr>
      <td>goToPage</td>
      <td>goToPage(page?,reload?)=>any</td>
      <td>跳转到目标页</td>
    </tr>
    <tr>
      <td>reload</td>
      <td>reload(isReload?)</td>
      <td>重新加载当前页，isReload设为true时，将重新加载分页</td>
    </tr>
    <tr>
      <td>pagingSize</td>
      <td>Number</td>
      <td>设置分页按钮生成的数量</td>
    </tr>
    <tr>
      <td>params</td>
      <td>Object</td>
      <td>设置查询参数</td>
    </tr>
    <tr>
      <td>invokeParam (可选)</td>
      <td>String</td>
      <td>调用后台接口参数隐射名，默认 `paging`</td>
    </tr>
    <tr>
      <td>total</td>
      <td>Number</td>
      <td>限制单个文件的大小</td>
    </tr>
    <tr>
      <td>currentPage</td>
      <td>Number</td>
      <td>当前第几页</td>
    </tr>
    <tr>
      <td>totalPage</td>
      <td>Number</td>
      <td>总页数</td>
    </tr>
    <tr>
      <td>hideDesc</td>
      <td>Boolean</td>
      <td>是否隐藏文字描述</td>
    </tr>
    <tr>
      <td>reloadAll</td>
      <td>Boolean</td>
      <td>是否总是重新加载分页</td>
    </tr>
  </tbody>
</table>
