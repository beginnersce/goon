# 0x01 工具介绍

> 我看到了一些零件，于是打算把他们拼接起来，这便有了goon。

> goon，是一款基于golang开发的扫描工具，暂时支持portscan、webscan、titlescan、dirscan、fofascan、pluginscan等模块功能，当然也支持将这些模块联动起来的autoscan。后期也会慢慢加入其他零件模块，感谢您的使用，也希望您能提供宝贵意见。

> 初次使用goon，请先运行一遍，会在当前目录下生成conf.yml。配置完conf.yml后便可正常使用。

# 0x02 模块特点
  
> -2.1、pluginscan 模块，自定义 yml 插件扫描，可以自定义指纹，也可以自定义 POC，可参考 plugin 下的 cms-zentao.yml 和 DSS-file-read.yml及demo/plugin.yml。  
> -2.2、autoscan 模块，自定义自动化扫描，可以将扫描模块联动起来。

# 0x03 开发环境

    go version go1.16.5 windows/amd64

# 0x04 模块介绍

## 0x041 portscan 模块

> portscan除了扫描端口外，还可以通过-web y命令来扫描http和https。

> 参数如下：

    -ip     :扫描IP，如:127.0.0.1、127.0.0.1/24、127.0.0.1-255
    -thread :默认从配置文件读取
    -ifile  :扫描文件，待扫描ip按行保存
    -ofile  :输出文件，默认保存到./result下
    -port   :扫描端口,如:80,443-445,8000-9000,默认从配置文件读取
    -web    :y表示扫描web(http、https)，n表示不扫描，默认为n
    
> 语法参考：

    goon_amd64_windows.exe -mode portscan -ip 127.0.0.1/24 -port 8000-10000
    goon_amd64_windows.exe -mode portscan -ifile ips.txt -thread 10000 -web y -ofile test.txt

## 0x042 titlescan 模块

> 扫描网站标题，目前可能会存在一些由于编码导致的乱码问题，后期会慢慢改进。

> 参数如下：

    -thread :默认从配置文件读取
    -ifile  :扫描文件，待扫描web按行保存
    -ofile  :输出文件，默认保存到./result下

> 语法参考：

    goon_amd64_windows.exe -mode titlescan -ifile web.txt

## 0x043 dirscan 模块

> dir扫描，根据返回code、返回header、返回body进行http判断。适用于临时验证某个资产指纹、简易POC等。

> 参数如下：

    -thread :默认从配置文件读取
    -ifile  :扫描文件，待扫描web按行保存
    -ofile  :输出文件，默认保存到./result下
    -dir    :要扫描的dir，如:/login.jsp
    -code   :请求返回的status_code，如:200、302，默认从配置文件读取
    -header :请求返回的header内容，如:rememberMe，默认从配置文件读取
    -body   :请求返回的body内容，如:root:x:0:0，默认从配置文件读取

> 语法参考：

    goon_amd64_windows.exe -mode dirscan -ifile webs.txt -dir "/zentao/index.php?mode=getconfig" -code 200 -body "version"

## 0x044 fofascan 模块

> fofa查询，可选择对fofa返回的host自动添加"http://"。

> 参数如下：

    -key    :查询语句，如:domain="fofa.so"
    -ifile  :扫描文件，待获取key按行保存
    -ofile  :输出文件，默认保存到./result下
    -num    :请求数量，如:100、10000，默认从配置文件读取
            智能模式只支持单个key获取方式。
    -fields :返回资产类型如:ip,port，默认从配置文件读取

> 语法参考：

    goon_amd64_windows.exe -mode fofascan -key port="8081" -num 100 -web y -fields host
    goon_amd64_windows.exe -mode fofascan -ifile keys.txt

## 0x045 pluginscan 模块

> 自定义yml插件扫描，yml可以是指纹，也可以是POC，详情见demo/plugin.yml。

> 参数如下：

    -thread :默认从配置文件读取
    -ifile  :扫描文件，待扫描web按行保存
    -ofile  :输出文件，默认保存到./result下
    -dpath  :plugin路径，可以是指定文件，也可以是指定目录，默认从配置文件中读取

> 语法参考:

    goon_amd64_windows.exe -mode pluginscan -ifile webs.txt -dpath ./plugin/cms-zentao.yml
    goon_amd64_windows.exe -mode pluginscan -ifile webs.txt

## 0x046 autoscan 模块

> 自定义扫描模块，在conf.yml中配置，y表示启动模块扫描。目前支持portscan、titlescan、pluginscan。在配置都为y的情况下，扫描资产web，然后将扫描结果result进行title扫描和plugin扫描。

> 参数如下：

    -ifile:扫描文件，ip按行保存

> 语法参考：

    goon_amd64_windows.exe -mode autoscan -ifile ips.txt
    

# 0x05 结语
  
> 1、感谢 key 佬和巨魔的宝贵建议  
> 2、欢迎各位师傅提供宝贵意见
=======
已删，之后发的版本不再支持fofa自动查询
>>>>>>> cb5ccdd44cbde638a7fac44e0573a7c174a17fe9
