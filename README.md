# 某9-未编译源码-ChatGPT-Web

某9演示站: https://ai.jiangly.com

### 服务器推荐
- [亚洲云 - 高防服务器|服务器租用|福州高防|广东电信|香港服务器|美国服务器|海外服务器 - 国内靠谱的企业级云计算服务提供商](https://www.asiayun.com/)

### 必要环境
- nodejs version > 16
- pnpm version > 6
- mysql version >= 5.7
- redis
### 目录结构
- chat 用户端代码
- admin 管理端代码
- service 服务端代码

## 本地开发
1. 进入 `service` 目录，创建 `.env` 文件，修改和测试数据库信息连接信息和 Redis 配置。
2. 数据库名称不能已经存在默认是chatgpt
3. redis、mysql 一定要先本地测试通，再保存.env文件
4. 上诉工作完成后执行：
```
pnpm i
pnpm dev
```
> 注意注意！这一步必须做,自动创建数据库,否则后面没有数据库、各种失败！

```
# 安装依赖
pnpm install

# 启动项目
pnpm dev

# 打包项目
pnpm build
```
### 三端统一命令
```
project-root
|-- chat           # 用户端代码
|-- admin          # 管理端代码
|-- service        # 服务端代码
```
### 启动项目
分别安装依赖并启动项目：
1. 进入 `chat` 目录，执行以下命令启动用户端：
```
pnpm i
pnpm dev
```
2. 进入 `admin` 目录，执行以下命令启动管理端：
```
pnpm i
pnpm dev
```
### 关于授权
授权模块位于 `src/modules/globalConfig/globalConfig.service.ts` 文件下。如果要移除授权，请清空 `nineAiCheckAuth` 函数内容，并移除 `onModuleInit` 中的 `nineAiCheckAuth`。
对应的定时任务也可以移除，位于 `src/modules/task/task.service.ts` 文件中的 `checkauth` 定时任务。
### 打包路径问题
#### 后端服务
后端服务只需执行以下命令即可：
```
pnpm build
```
生成七个文件，其中 `.env` 是环境变量文件，需要在后续部署时自行挂载或创建。项目提供示例文件 `.env.example`。

#### chat（前端项目）
前端项目打包使用配置文件 `.env.production`，与 `admin` 相同。修改文件中的变量即可，如果分开部署，请填写线上后端服务地址。

#### admin（管理端）
管理端与 chat 部署方式相同，修改 `.env.production` 中的配置即可。分离部署时，只需替换线上地址，其余配置暂时用不到。

### 其他文件


#### 后端服务打包后需要这七个文件

- chat:前端项目打包的配置文件是.env.production 和admin相同

- 只需要改变这个变量 如果分开部署的则填写你的线上后端服务地址 建议分开 第一行地址填写这个自己的线上地址就行

- admin:管理端是同理、一样修改这个文件

- 同样分离部署只需要打开红框的内容即可、替换为自己的线上地址 其余配置并不需要修改 也暂时用不到

### 其他问题
刷新404问题:前端history项目刷新都会404 需要对nginx进行配置

### 效果图如下
#### 用户界面
![用户界面](https://github.com/vpsad/NineAi-ChatGPT-Web-Code-Free/blob/main/nine-user.jpg?raw=true)
#### 管理界面
![管理界面](https://github.com/vpsad/NineAi-ChatGPT-Web-Code-Free/blob/main/nineadmin.jpg?raw=true)
