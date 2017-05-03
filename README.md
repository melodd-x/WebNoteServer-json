<h1 align=center >WebNoteServer</h1>

[![](https://img.shields.io/badge/download-5K-brightgreen.svg)](https://github.com/melodd-x/WebNoteServer.git)
![](https://img.shields.io/badge/body--parser-1.4.3-blue.svg)
![](https://img.shields.io/badge/express-4.4.5-blue.svg)

<h2 align=center >WebNoteServer-(JSON)接口文档</h2>

- WebNote json文件存储服务器
- Author:汪潇凯
- Email:<melodd@yeah.net>



### 使用方法
1. 下载ZIP压缩包,并且解压
2. 用CMD或终端进入项目目录,安装项目所需的依赖包`npm install`
3. 安装完成后,`node server.js`或`npm start` 运行
4. 获取的数据和提交的数据都在`comments.json`

### 修改接口和数据
1. `app.set('port', (process.env.PORT || 7428));`
7428就是端口号,根据需求自己改,完整地址:http://127.0.0.1:7428/api/comments
> 如果服务器给多人使用,主域名改成局域网的主域名即可.
>
> 比如:http://192.168.1.141:7428/api/comments
2. 默认数据:
```javascript
id: req.body.id,
title: req.body.title,
date: req.body.date,
content: req.body.content,
markdown: req.body.markdown
```

### 数据说明
- `id`:就是数据id,前端给
- `title`:文章标题
- `data`:文章的创建时间或上传时间
- `content`:.md->html->文本,两次解析后的数据(根据需求是否需要)
- `markdown`: 用户输入的markdown内容


### 前端
> 如果使用vue.js的axios进行请求

##### 1.请求服务器数据

```javascript
mounted() {

        axios.get('http://127.0.0.1:7428/api/comments')
            .then(function(response) {
                console.log(response.data);
                this.$store.state.notes = response.data;
            }.bind(this))
            .catch(function(error) {
                console.log(error);
            });
    }
```

##### 2.提交数据给服务器
```javascript
addNote(state, note) {

    axios({
        method: 'post',
        url: 'http://127.0.0.1:7428/api/comments',
        data: {
            id: note.id,
            title: note.title,
            date: note.date,
            content: note.content,
            markdown: note.markdown
        },
        transformRequest: [function(data) {
                // Do whatever you want to transform the data
                let ret = ''
                for (let it in data) {
                    ret += encodeURIComponent(it) + '=' + encodeURIComponent(data[it]) + '&'
                }
                return ret
            }
        ]
    });
```

###### 2.1 使用qs( 使用之前需要引入qs模块 )

```javascript
import qs from 'qs'
```

```javascript
axios.post('http://127.0.0.1:7428/api/comments',qs.stringify({
          id:id,
          title:title,
          date:dat,
          content:content
        }))
```

> 有任何疑问或者意见,请联系我


![](https://img.shields.io/github/watchers/badges/shields.svg?style=social&label=Watch)
