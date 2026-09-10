# 参与 FinLedger Pro

[English](CONTRIBUTING.md) | [简体中文](CONTRIBUTING.zh-CN.md)

FinLedger Pro 是一个教学型项目。作者通过亲自实现每一个模块学习软件工程、财务和会计，因此所有应用代码都由作者本人编写。

所有被接受的贡献都按照仓库的 MIT 许可证发布，不要求贡献者转让版权。详见[永久开源与免费承诺](OPEN_SOURCE_COMMITMENT.zh-CN.md)。

## 欢迎的贡献

| 贡献类型 | 是否欢迎 |
|---|---|
| Bug 报告 | 欢迎 |
| 架构建议、产品建议和会计纠错 | 欢迎 |
| 文档错别字、表达和链接修正 | 欢迎 |
| 关于设计或财务概念的问题 | 欢迎 |
| 实现功能或重构应用代码的 PR | 不纳入主项目 |

如果发现实现错误，请提交问题并说明复现步骤、预期结果和实际结果，而不要直接替作者完成实现。你可以根据 MIT 许可证开发私有或商业下游软件。公司定制优先建立独立私有仓库并依赖公开核心的正式版本；只有无法通过扩展契约表达时才维护 fork。详见[公开核心与公司私有仓库](docs/public-core-and-private-company-repos.zh-CN.md)。

## 隐私要求

不要上传真实财务数据、数据库、导出文件或带有真实余额的截图。请使用虚构数据复现问题。安全漏洞不要提交公开问题，应通过 GitHub Security Advisory 私下报告。

## 文档规范

- 按照[开发环境配置](docs/development-setup.zh-CN.md)使用仓库锁定的工具链和本地环境。
- 主要文档成对维护英文和简体中文版本。
- 如果两个版本暂时不一致，以英文技术表述为准。
- 修改含义时应在同一次提交中更新两种语言。
- 代码注释始终使用英文。
- 金额始终使用 `Decimal`，不使用 `float`。
- `personal/` 和 `pro/` 可以依赖 `core/`，但不能互相依赖。
- 公司私有仓库可以依赖公开核心正式版本，公开核心不得反向依赖私有代码。
- 银行供应商只能读取账户、余额和流水，不得包含付款、批量付款、收款人、在线收款或银行卡控制能力。

## 阅读入口

- [中文 README](README.zh-CN.md)
- [中文系统架构](docs/architecture.zh-CN.md)
- [中文产品路线图](docs/product-roadmap.zh-CN.md)
- [中文 Xero 功能借鉴](docs/xero-product-benchmark.zh-CN.md)
- [中文开放 API 与多币种策略](docs/open-api-and-multi-currency.zh-CN.md)
- [公开核心与公司私有仓库](docs/public-core-and-private-company-repos.zh-CN.md)
- [永久开源与免费承诺](OPEN_SOURCE_COMMITMENT.zh-CN.md)
- [中文变更日志](CHANGELOG.zh-CN.md)
