# Generator API

## cliVersion

类型：`string`

调用插件时的**全局**`@vue/cli`版本号。


## assertCliVersion

- **参数**
  
  - `{integer | string} range` -  `@vue/cli` 需要满足的semver版本号范围
  
- **用途**

  声明版本号有时是很有用的，而此处通过这种简单的方式实现了。
  
  如果版本号满足要求那什么也不会发生，否则就会抛出错误。


## cliServiceVersion

类型: `string`

调用插件的 **项目局部**的 `@vue/cli-service` 版本号。


## assertCliServiceVersion

- **参数**
  
  - `{integer | string} range` -  `@vue/cli-service` 需要满足的semver版本号范围
  
- **用途**

  该API提供了一个简单的方式去声明本地项目要求的 `@vue/cli-service` 版本号。

  如果版本号满足要求那什么也不会发生，否则就会抛出错误。

  注意: 大多数情况下推荐使用 [ `package.json` 中的 `peerDependencies` 字段](https://docs.npmjs.com/files/package.json#peerdependencies)。


## resolve

- **参数**
  - `{string} ..._paths` - 路径或路径片段的序列。

- **返回值**
  - `{string}`- 基于项目根目录而解析的绝对路径。

- **用途**:
  把一个路径或路径片段的序列解析为一个绝对路径。

## hasPlugin

- **参数**
  - `{string} id` - 插件 id,  可忽略  (@vue/|vue-|@scope/vue)-cli-plugin- 前缀
  - `{string} version` - semver 版本号范围, 选填
  
- **返回值**
  - `{boolean}`
  
- **用途**:

  检查当前项目是否包含指定id的插件，如果给出了版本号，那么就需要满足给定的版本号。

## addConfigTransform

- **参数**
  - `{string} key` - package.json文件中的配置 key。
  - `{object} options` - 选项
  - `{object} options.file` - 文件描述符. 用于搜索已经存在的文件，每一个key都是一种文件类型，（可能的文件类型：['js', 'json', 'yaml', 'lines']），该值是一个文件名的列表。
  例如：
  ```js
  {
    js: ['.eslintrc.js'],
    json: ['.eslintrc.json', '.eslintrc']
  }
  ```
  
默认，使用第一个文件名创建配置文件。
  
- **返回值**
  
  - `{boolean}`
  
- **用途**:
  配置提取项目配置文件。

## extendPackage

- **参数**
  
  - `{object | () => object} fields` - 用来合并的字段
  
- **用途**:

  扩展项目 `package.json` 。嵌套字段将递归合并，除非设定了 `{ merge: false }`，而且会解决插件间的依赖冲突。在将文件写入磁盘之前，可以将工具配置字段提取到独立文件中。

## render

- **参数**
  
  - `{string | object | FileMiddleware} source` - 可以是以下之一
    - 某目录的相对路径;
    -  `{ sourceTemplate: targetFile }` 模式的哈希映射;
    - 一个定制的文件中间件函数
  - `{object} [additionalData]` - 用于模板文件的可选数据
  - `{object} [ejsOptions]` - ejs选项
  
- **用途**:

  渲染模板文件到虚拟文件树对象

## postProcessFiles

- **参数**
  
  - `{FileMiddleware} cb` - 文件中间件
  
- **用途**:

  在所有正常的文件中间件被应用之后插入一个文件中间件

## onCreateComplete

- **参数**
  
  - `{function} cb`
  
- **用途**:

  文件写入磁盘之后的回调函数。

## exitLog

- **参数**
  
  - `{} msg` - 生成器完成后输出的字符串或值。
  - `{('log'|'info'|'done'|'warn'|'error')} [type='log']` - 信息类型.
  
- **用途**:

  在生成器退出后输出一条信息（在所有标准信息之后）。

## genJSConfig

- **参数**
  
  - `{any} value`
  
- **用途**:

  从JSON中生成一个JS配置文件。

## makeJSOnlyValue

- **参数**
  
  - `{any} str` - 字符串类型的JS表达式
  
- **用途**:
  Turns a string expression into executable JS for .js config files

  字符串表达式转换为可执行的JS，用于.js配置文件。

## injectImports

- **参数**
  - `{string} file` - 目标文件添加imports 
  - `{string | [string]} imports` - imports string/array
- **用途**:
添加import语句到一个文件。



## injectRootOptions

- **参数**
  
  - `{string} file` - 目标文件添加选项
  - `{string | [string]} options` - options string/array
  
- **用途**:

  为root Vue实例时添加选项（依据 new Vue）

## entryFile

- **返回值**
  
  - `{('src/main.ts'|'src/main.js')}`
  
- **用途**:

  获取入口文件（考虑到typescript）

## invoking

- **返回值**
  - `{boolean}`

- **用途**:
  检测插件是否已经被调用.

