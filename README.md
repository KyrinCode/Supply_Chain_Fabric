该项目依赖 go 语言环境、docker 环境，自行安装配置；

`go_supplychain` 目录作为 `$GOPATH`，需要改变为 go 配置的环境变量，整个目录架构不可改变；

`go_supplychain⁩/⁨src⁩/github.com⁩/hyperledger⁩/fabric⁩` 目录是超级账本框架；

`go_supplychain⁩/⁨src⁩/github.com⁩/hyperledger⁩/fabric⁩-sdk-go` 目录是 Go Web 调用 fabric 的 SDK；

`go_supplychain⁩/⁨src⁩/github.com⁩/hyperledger⁩/fabric⁩/supplychain` 目录是本项目的工作目录；

其中 `deploy` 目录中为 fabric 网络的配置和启动文件、`chaincode` 目录中为实现供应链业务逻辑的链码、`application` 目录中为 Go Web 微框架 Gin-gonic 的后端及前端页面；

`deploy/config` 和 `deploy/crypto-config` 分别存有网络搭建中的区块交易文件、排序节点记账节点CA的身份信息；

`deploy` 目录中其他配置文件参考 `Supply_Chain 搭建详解.md`，这里简要说明：排序组织对应管理组织、组织 0 对应原料商有 1 个节点用来上传原料信息、组织 1 对应加工商有 1 个节点用来上传加工信息和商品信息、组织 2 对应物流商有 1 个节点用来上传物流信息、组织 3 对应销售商第 1 个节点用来上传销售信息第 2 个节点用来开放给消费者查询商品信息；

`chaincode/sourceTrace` 中 `requirements.md` 中为业务的实现逻辑，`sourceTrace.go` 链码中有每项业务实体和功能的详细注释；

`application/html` 中为登录页和各用户登录对应的界面，由于注册是在 fabric 配置网络过程中进行的，在此直接赋予每个用户身份（`Material`、`Process`、`Express`、`Sale`、`Customer`，密码均为 `****`）供直接登录（这部分想要修改的话，在 `main.go` 中第 49 行的 `userLogin` 函数中修改），`config.yaml` 文件中为 SDK 的配置；（注：此处添加注册界面说不通，因为底层区块链网络在搭建时已确定各参与组织，没有必要在前端设置注册页面）

测试用例中，将每次上传的信息抽象成了各种 `info`，根据需要自行替换成具体的原料信息、加工信息、物流信息、销售信息等。

