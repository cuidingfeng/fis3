## 安装

### 安装 Node 和 NPM

详细过程参考官网 https://nodejs.org

- Ubuntu 用户使用 `apt-get` 安装 node 后，安装的程序名叫 `nodejs`，需要软链成 `node`
- Windows 用户安装完成后需要在 CMD 下确认是否能执行 node 和 npm

### 安装 FIS3

```bash
npm install -g fis3
```
- `-g` 安装到全局目录，必须使用全局安装，当全局安装后才能在命令行（cmd或者终端）找到 `fis3` 命令
- 安装过程中遇到问题具体请参考 https://github.com/fex-team/fis/issues/565 解决

### 升级 FIS3

```bash
npm update -g fis3
```
或重装
```
npm update -g fis3
```