## 调试

FIS3 构建后，默认情况下会对资源的 URL 进行修改，改成绝对路径。这时候本地双击打开文件是无法正常工作的。这给开发调试带来了绝大的困惑。

FIS3 内置一个简易 Web Server，可以方便调试构建结果。

### 目录

构建是不指定输出目录，即不指定 `-d` 参数时，构建结果被发送到内置 Web Server 的根目录下。此目录可以通过执行一下命令打开。

```bash
fis3 server open
```

### 发布

```bash
fis3 release
```

不加 `-d` 参数默认被发布到内置 Web Server的根目录下，当启动服务时访问此目录下的资源。

### 启动

通过

```bash
fis3 server start
```
来启动本地 Web Server，当此 Server 启动后，会自动浏览器打开 `http://127.0.0.1:8080`，默认监听端口 `8080`

通过执行以下命令得到更多启动参数，可以设置不同的端口号（当 `8080` 占用时）

```bash
fis3 server -h
```

### 预览

启动 Web Server 以后，会自动打开浏览器，访问 `http://127.0.0.1:8080` URL，这时即可查看到页面渲染结果。正如所有其他 Web Server，<font color="red">FIS3 内置的 Server 也是常驻的，如果不重启计算机或者调用命令关闭</font>。

所以后续只需访问对应链接即可，而不需要每次 `release` 就启动一次 `server`。

### 文件监听

为了方便开发，FIS3 支持文件监听，当启动文件监听时，修改文件会构建发布。而且其编译是增量的，编译花费时间少。

FIS3 通过对 `release` 命令添加 `-w` 或者 `--watch` 参数启动文件监听功能。

```bash
fis3 release -w
```
> 添加 `-w` 参数时，程序不会马上执行；停止程序用快捷键 <kbd>CTRL</kbd>+<kbd>c</kbd>

### 浏览器自动刷新

文件修改自动构建发布了，如果浏览器能自动刷新，这是一个非常好的体验。

FIS3 支持浏览器自动刷新功能，只需要给 `release` 命令添加 `-L` 参数，通常 `-w` 和 `-L` 一起使用。

```bash
fis3 release -wL
```

> 程序停止用快捷键 <kbd>CTRL</kbd>+<kbd>c</kbd>

### 替代内置Server

FIS3 内置了一个 Web Server 提供给构建后的代码进行调试。如果你自己启动了你自己的 Web Server 依然可以使用它们。

假设你的 Web Server 的根目录是 `/Users/my-name/work/htdocs`，那么发布时只需要设置产出目录到这个目录即可。

```bash
fis3 release -d /Users/my-name/work/htdocs
```
当访问你的 Web Server 监听的端口，即可访问调试。

如果想执行 `fis3 release` 直接发布到此目录下，可在配置文件配置；

```js
fis.match('*', {
  deploy: fis.plugin('local-deliver', {
    to: '/Users/my-name/work/htdocs'
  })
})
```