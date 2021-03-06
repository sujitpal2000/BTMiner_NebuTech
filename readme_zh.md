# BTM GPU挖矿软件（BTMiner_NebuTech）

用于Nvidia显卡的`Bytom(比原链)`挖矿软件。

## 下载地址

[从这里下载](https://github.com/NebuTech/BTMiner_NebuTech/releases)

## 功能特点：

- 支持Win7、Win10、Linux
- 支持标准stratum协议的矿池
- 不占用CPU和PCI-E带宽，现有6卡、8卡矿机适用
- **从v5.0开始只支持10代及以后的N卡，前代卡请使用老版本软件**
- 包含3%开发手续费，可以通过选项关闭

## 使用方法：

1. **驱动版本，Windows大于等于385, Ubuntu大于384**
2. 编辑`start_cmd.bat`文件(Linux系统修改`start_cmd.sh`)，修改`-url`后面的矿池地址和`-user`后面的钱包地址或用户名。如果有密码，添加`-p`参数和密码。
3. Windows双击运行`start_cmd.bat`开始挖矿, Linux通过命令行运行`start_cmd.sh`开始挖矿。

## 参考显卡性能

- **注：以下参数均为显卡默认频率功耗下的测试数据**

| 显卡    | 参考算力（H/s） |
| ------- | --------------- |
| 1030    | 210             |
| 1050    | 370             |
| 1050Ti  | 450             |
| 1060-3G | 700             |
| 1060-6G | 760             |
| 1070    | 1100            |
| 1070Ti  | 1400            |
| 1080    | 1530            |
| 1080Ti  | 2100            |
| Titan V | 4200            |

## 命令行参数：

BTMiner_NebuTech [参数]

**典型用法**：BTMiner_NebuTech -url btm.f2pool.com:9221 -user bm1xxxxxxxxxxxx.rigName

参数：

- -?, -h, --help    显示帮助信息.
- -v, --version    显示版本号.
- -c, --config \<config file path>    通过配置文件启动挖矿程序.
- --api \<host:port>    REST API监听端口.
- -B, --browser    自动打开网页监控页面。仅适用于windows。
- -o, --url \<url>    矿池地址.
- -u, --user \<user>    挖矿使用的用户名或钱包地址.
- -p, --passwd \<password>    挖矿使用的密码.
- -d, --devices \<devices>    指定使用哪些显卡来挖矿. 比如: "-d 0,1,2,3" 使用前4个显卡.
- -S, --ssl    使用SSL连接矿池（需矿池支持）
- --log    生成日志文件，文件名为 `log_<时间戳>.txt`.
- --long-format    使用更长的日期时间格式
- --no-fee    关闭开发者手续费，同时会关闭部分优化，算力有所下降。

## GPU配置建议

Bytom挖矿主要依靠GPU核心，矿工在实际挖矿中可以通过MSI Afterburner等工具将显存调整为-500，基本不会影响BTM的挖矿算力（以实测为准）。

甚至如果设置了例如80%的功耗限制，降低显存设置可以带来算力提升（因为功耗限制，降显存频率以后可以有更多的电能共给到GPU核心）。

## API查询接口

### 网页监控

在浏览器中打开 http://api_host:port/ 启动网页监控.

### 请求

GET http://api_host:port/api/v1/status

### 返回

```json
{
    "kernel_reboot_times": 0,
    "miner": {
        "devices": [{
            "core_clock": 1556,
            "core_utilization": 100,
            "fan": 36,
            "hashrate": 1499,
            "id": 0,
            "info": "GeForce GTX 1080 Ti 11178 MB",
            "power": 182,
            "temperature": 65
        }, {
            "core_clock": 1518,
            "core_utilization": 100,
            "fan": 34,
            "hashrate": 1490,
            "id": 1,
            "info": "GeForce GTX 1080 Ti 11178 MB",
            "power": 172,
            "temperature": 62
        }],
        "total_hashrate": 2989,
        "total_power_consume": 354
    },
    "start_time": 1532482659,
    "stratum": {
        "accepted_share_rate": 0.99,
        "accepted_shares": 99,
        "password": "",
        "rejected_share_rate": 0.01,
        "rejected_shares": 1,
        "url": "btm.pool.zhizhu.top:3859",
        "use_ssl": false,
        "user": "bmxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx.test"
    },
    "version": "v7.0"
}
```

## 开发计划

- 完善对显卡异常的处理
- 提高算力
- 不再进行GUI版本开发，推荐使用集成了我们的BTMiner，功能更加丰富的软件：[深圳矿工](http://www.szminer.net/)（WIndows）、[矿山系统](http://40451.net/)（Linux）、[MinerOS](https://www.mineros.cn/#/)（Linux）

## 致谢

@earthGavinLee

## 修改记录

#### v7.0(2018-08-03)

- 提高20%左右算力
- 增加长日期时间格式输出的选项
- 增加日志文件输出的选项
- 取消`-M`选项
- 稳定性修复

#### v6.0(2018-07-23)

- 增加状态查询的API接口
- 增加状态监控的web页面
- 增加更多的GPU状态信息查询：功耗、核心频率、核心使用率
- 底层参数调整，部分机器2-3%的算力提升
- 运行时检查对矿池提交对应的应答数，防止矿池无响应现象出现
- 优化控制台日志输出格式

#### v5.1(2018-07-07)

* 禁用CMD快速编辑模式，防止进程被冻结
* 禁止程序崩溃时弹出windows错误报告

#### v5.0(2018-07-03)

- 大幅提高算力
- 可使用配置文件启动
- 增加使用SSL矿池连接的选项
- 增加关闭手续费的选项
- 取消CPU模式的选项
- 取消GUI壳程序（后续不在更新）

#### v3.3(2018-06-16)

- GUI界面增加配置自动保存恢复功能
- (GUI)Add auto saving config
- 修复经常崩溃的bug，提升稳定性。 
- Fix Crash, 

#### v3.0(2018-06-09)

- 大幅提升算力
- 自动优化选择上个版本的`-i`参数
- 增加`-M`选项，应对多卡时可能出现的`CUDA out of memory error`
- Windows增加图形界面壳程序，便于新手操作
- 图形界面增加公告，获取最新版本通知
- 修复已知BUG，提升稳定性。

#### v2.0(2018-06-04)

- 进一步降低CPU使用率。
- 增加针对高端CPU及高PCIE带宽的加速模式。
- 支持Linux
- 修复已知BUG，提升稳定性。

#### v1.3(2018-06-03)

- 第一版。
- 支持Windows。
- 优化CPU、PCI-E带宽占用。
- 优化挖矿速度。
- 支持标准stratum协议。