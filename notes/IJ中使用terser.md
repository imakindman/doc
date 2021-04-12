### 在IntelliJ IDEA中使用terser对js文件进行压缩处理

> 不仅terser，uglifyjs等工具也可以参照如下配置。

#### 配置步骤：

+ IDEA版本：Ultimate 2020.2。

+ npm安装terser。

+ 依次打开`File` -> `Settings` -> `Tools` -> `External Tools` -> 点击 `+` 打开新增面板填写配置信息。

+ 基本信息：  

  `Name`：工具名称，这里推荐使用原名。  
  
  `Descriptions`: 工具描述。  

+ 工具配置（`Tool Settings`）：  

  `Program`：填写工具地址，terser.cmd文件的资源路径（举例：C:\Users\zhangsan\AppData\Roaming\npm\terser.cmd）。  
  
  `Arguments`：参数配置（$FileName$ -o $FileNameWithoutExtension$.min.js）。  
  
  `Working directory`：工作目录（$FileDir$）。  
 
+ 配置完成。

#### 使用方法

右击选择要处理的js文件，在弹出的右键菜单中 -> 选择`External Tools` -> 选择terser（你填写的工具名称）即可。


