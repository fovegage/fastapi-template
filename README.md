## 说明

```
# opentome cms管理系统

1. 以套餐包的形式向用户收费
2. 每个模块有免费的额度
3. 如果继续体验 需要购买付费包
    1. opentoem.cn 只提供基本能力
    2. 付费包 参考百望设计  在 ai/wetool.opentome.cn
    3. https://www.baiwang.com/personalCenter/#/online-renew
4. 该项目使用python开发  方便进行整合   不用在启动serveless
    1. 可以私有化部署
    2. 所有功能 尽可能不调用接口
    3. 不调用 opentome接口 封装 直接调用大模型接口
    4. 为了宣传 非私有化部署调用 golang封装的serverless 私有化部署全python实现
5. 只有一个管理员 可以接入sso鉴权
```

## 产品

```
1. 票据识别 字段标注
```

## 开发

```
uv sync --frozen
.\.venv\Scripts\activate

fastapi dev main.py
uvicorn main:app --reload
```

## mysql

```
# 注意数据库编码
CREATE DATABASE wetool
  DEFAULT CHARACTER SET utf8mb4
  COLLATE utf8mb4_general_ci;
```

## 说明

```
# 支持用户注册  支持配置 llm key、opentome key
# opentome.cn 只进行计费
# 该系统单独鉴权？？

1. 租户管理 rbac
2. 部分功能开源
3. 单独的账户体系
4. 可以私有化部署
```

## 文档

```
文档可以借鉴 vben的
```