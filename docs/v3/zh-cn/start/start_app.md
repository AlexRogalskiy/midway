# 创建第一个应用

## 关于 v3

当前 v3 版本还是 beta 状态，在未发布前，我们依旧会调整 API 并且无法及时通知用户，但是相应的，可以随时使用到最新的功能。

## 快速初始化


```bash
$ npm -v

# 如果是 npm v6
$ npm init midway --type=koa-v3 my_midway_app

# 如果是 npm v7
$ npm init midway -- --type=koa-v3 my_midway_app
```

`my_midway_app`  是你即将创建的项目根目录名，CLI 会自动创建该目录，并将初始化示例代码写入其中。

注意，下图的命令和上面不一样，等 v3 正式发布后我们会重录。

流程示例如下（npm7 效果）：

![create.svg](https://img.alicdn.com/imgextra/i3/O1CN01SKMFSB1Utr04ArZXJ_!!6000000002576-55-tps-1390-776.svg)

:::info
可以使用 `npm init midway` 查看完整的脚手架列表，选中某个项目后，Midway 会自动创建示例目录，代码，以及安装依赖。
:::


![create-with-cli.svg](https://img.alicdn.com/imgextra/i4/O1CN016efif51uI0HFO9RWh_!!6000000006013-55-tps-1770-928.svg)

示例将创建一个类似下面的目录结构，其中最精简的 Midway 项目示例如下。

```
➜  my_midway_app tree
.
├── src                            ## midway 项目源码
│   └── controller                 ## Web Controller 目录
│       └── home.controller.ts
├── test
├── package.json
└── tsconfig.json
```
整个项目包括了一些最基本的文件和目录。


- `src`  整个 Midway 项目的源码目录，你之后所有的开发源码都将存放于此
- `test` 项目的测试目录，之后所有的代码测试文件都在这里
- `package.json`  Node.js 项目基础的包管理配置文件
- `tsconfig.json`  TypeScript 编译配置文件


除了整个目录，我们还有一些其他的目录，比如 `controller` 目录。


## 开发习惯


Midway 对目录没有特别的限制，但是我们会遵守一些简单的开发习惯，将一部分常用的文件进行归类，放到一些默认的文件夹中。


以下 ts 源码文件夹均在 `src` 目录下。


常用的有：


- `controller` Web Controller 目录
- `middleware` 中间件目录
- `filter` 过滤器目录
- `aspect` 拦截器
- `service` 服务逻辑目录
- `entity` 或 `model`  数据库实体目录
- `config` 业务的配置目录
- `util` 工具类存放的目录
- `decorator` 自定义装饰器目录
- `interface.ts`  业务的 ts 定义文件



随着不同场景的出现，目录的习惯也会不断的增加，具体的目录内容会体现在不同的框架中。




## Web 框架选择


Midway 设计之初就可以兼容多种上层框架，比如常见的 `Express`、`Koa` 和 `EggJS` 。

从 v3 开始，我们使用 Koa 来做基础示例的演示。

这些上层框架都可以使用 Midway 提供的装饰器能力，但是 Midway 不会对特有的能力做出封装，比如 Egg.js 的插件体系，或者 Express 的中间件能力，如果你对其中的某个框架比较熟悉，或者希望使用特定框架的能力，就可以选择它作为你的主力 Web 框架。


| 名称 | 描述 |
| --- | --- |
| @midwayjs/koa | 默认，Koa 是一个 Express 的替代框架，它默认支持了异步中间件等能力，是第二大通用的 Node.js Web 框架。 |
| @midwayjs/web | Egg.js 是国内相对常用的 Web 框架，包含一些默认插件。 |
| @midwayjs/express | Express 是一个众所周知的 node.js 简约 Web 框架。 这是一个经过实战考验，适用于生产的库，拥有大量社区资源。  |


如果你希望替代默认的 Web 框架，请参考对应的框架章节。

## 启动项目


```bash
$ npm run dev
$ open http://localhost:7001
```
Midway 会启动 HTTP 服务器，打开浏览器，访问 `http://127.0.0.1:7001` ，浏览器会打印出 `Hello midwayjs!`  的信息。


![image.png](https://img.alicdn.com/imgextra/i2/O1CN01KoUxO91jydMw41Vv4_!!6000000004617-2-tps-1268-768.png)


如果需要修改开发的启动端口，可以在 `package.json`  的 scripts 段落里修改，如修改为 6001：

```typescript
"scripts": {
  //...
  "dev": "cross-env ets && cross-env NODE_ENV=local midway-bin dev --ts --port=6001",
},
```

## 常见问题

### Python 的编译错误

:::warning
1、在 node15/npm7 下执行 `npm install/i` 命令安装依赖可能会有 Python 编译错误

**使用 npm init midway 创建的项目会自动安装依赖，无此问题。**

**解决方案**：npm i 时添加 `--legacy-peer-deps`  参数。
**原因**：测试框架 Jest 依赖 jsdom，npm7 会自动安装其 peerDependencies 中依赖的 canvas 包， 而 canvas 的安装编译需要有python3环境。
:::

### Deprecated 提示

:::warning
2、在安装依赖时会有 npm warn: deprecated 输出


**原因**：测试框架 Jest 依赖 jsdom，其依赖了已废弃的模块 request，目前jsdom尚未解决此问题，我们会持续进行跟踪，相关问题参看：[https://github.com/jsdom/jsdom/issues/2792](https://github.com/jsdom/jsdom/issues/2792)
:::

### windows eslint 报错

:::warning
3、windows 可能会碰到 eslint 报错的问题，请关注 [windows 下换行问题](git_problem#XCAgm)。
:::
