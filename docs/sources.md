# 官方资料与核对说明

核对日期：2026-10-17

[项目首页](../README.md) · [完整报告](agent-sandbox-competitive-analysis.md)

## 一手资料

| 产品 | 官方来源 | 支持的范围 |
| --- | --- | --- |
| E2B | [产品能力](https://e2b.dev/) · [定价](https://e2b.dev/pricing) · [SDK 源码](https://github.com/e2b-dev/E2B) | microVM、生命周期能力、套餐、资源单价及兼容参照 |
| Daytona | [Sandbox](https://www.daytona.io/docs/en/sandboxes/) · [隔离](https://www.daytona.io/docs/en/isolation/) · [计费](https://www.daytona.io/docs/billing) · [价格](https://www.daytona.io/pricing) | 容器/VM 类别、网络策略、生命周期分状态计费及标价 |
| Modal | [Sandboxes](https://modal.com/products/sandboxes) · [资源和计费](https://modal.com/docs/guide/sandbox-resources) · [网络与安全](https://modal.com/docs/guide/sandbox-networking) | 物理 CPU 单位、`max(request, actual)`、gVisor/VM 与出口控制 |
| AWS AgentCore | [定价与计算形态](https://aws.amazon.com/bedrock/agentcore/pricing/) · [开发者指南](https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/) | 实际消耗计费、Runtime v2 内存回收、Instances 与治理模块 |
| Vercel | [Sandbox 定价和配额](https://vercel.com/docs/sandbox/pricing) | 活跃 CPU、预置内存、区域和其他计费项目 |
| Cloudflare | [Sandbox 文档入口](https://developers.cloudflare.com/sandbox/) | 后续核对入口；本次未独立复核原稿价格数字 |
| Kubernetes Agent Sandbox | [官方 SIG 项目仓库](https://github.com/kubernetes-sigs/agent-sandbox) | Sandbox、Template、Claim、WarmPool 等资源抽象 |
| 阿里云 | [E2B 迁移与兼容](https://help.aliyun.com/zh/functioncompute/e2b-compatibility-and-migration) · [实例隔离与浅休眠](https://www.alibabacloud.com/help/zh/functioncompute/overview-of-instance-isolation) · [深休眠](https://help.aliyun.com/en/functioncompute/sandbox-deep-hibernation-pause-and-resume-session) | 兼容范围、FC 扩展、浅休眠内存收费、深休眠前提 |
| 腾讯云 | [Agent Runtime](https://cloud.tencent.com/product/ags) · [CubeSandbox](https://github.com/TencentCloud/CubeSandbox) | 平台分层、产品性能宣称、开源底座与测试口径 |
| 火山引擎 | [沙箱模板概述](https://docs.volcengine.com/docs/agentkit/Tool_overview?lang=zh) · [模板管理](https://docs.volcengine.com/docs/agentkit/Creating_tools?lang=zh) · [AgentKit](https://docs.volcengine.com/docs/agentkit?lang=zh) | microVM、工具实例生命周期及 AIO/Code/Skills 模板 |

这些来源用于追溯具体说法，不表示本文已把所有产品功能、区域和版本逐项测试。

## 价格与口径

| 项目 | 本次状态 |
| --- | --- |
| E2B CPU/内存小时价 | 官方秒价乘 3600：0.000014 × 3600 = 0.0504；0.0000045 × 3600 = 0.0162 |
| Daytona CPU/内存小时价 | 官方价格页直接列出 $0.0504/vCPU·时、$0.0162/GiB·时 |
| Modal CPU 参考价 | 产品页物理核秒价 0.00003942 × 3600 / 2 = 0.070956，约 0.0710/等效 vCPU·时；不据此换算内存 |
| Modal 内存价与套餐 | 保留原稿参考，未在本次发布核对中逐项确认；采购前复核 |
| AWS v2 与 Code Interpreter | 官方定价分别列出对应 CPU 与内存值；保留官方 GB 单位 |
| Vercel CPU/内存 | 定价页默认区域值；保留官方 GB 单位，不混称 GiB |
| Cloudflare 数字 | 原稿参考，未独立复核，不作为确定的低价排序证据 |
| 国内产品 | 不把宣传文章中的单价混入跨区域、跨币种比较 |

## 发布核对记录

保留原稿的框架、产品范围与 P0/P1/P2 建议。以下是为公开阅读作出的事实边界和可追溯性修订：

1. **“E2B 已成为事实标准”改为带依据的分析判断。** 官方兼容文档证明存在兼容路径，不证明完整 API 同构、全行业采用率或正式标准地位。
2. **迁移说明补充高级能力差异。** Endpoint/API Key 配置不能替代 Snapshot、Volume、网络、权限等验收。
3. **补充火山引擎 microVM 说明。** 当前官方模板概述已明确该隔离基础，更新原稿“未找到说明”的状态。
4. **收紧成本倍数。** “10 分钟活跃 + 50 分钟闲置”的 6 倍只对应按存活时长计费、规格不变、无固定费用的计算资源项；不等于所有产品总月账单都增加 6 倍。
5. **补充内存与停机费用。** CPU 等待免计费不意味着整单免费；Daytona 停止/暂停/归档与阿里云浅/深休眠分别处理。
6. **不把 GB 和 GiB 混作同一单位。** 不把 Modal 物理核单价直接与 vCPU 单价排序。
7. **区分模型网关与工具网关。** AgentCore Gateway 的工具治理不能不加说明地充当多模型路由能力依据。
8. **限定性能宣称。** 创建、恢复、预热分配及单并发/高并发尾延迟不混比；CubeSandbox 的裸金属测试条件单独说明。
9. **不下无证据排名。** 未保留“列表价最低”“所有产品都趋同”或“容器/gVisor 一定弱且不安全”的绝对结论。
10. **移除缺图引用。** 原文 Fly Sprites 图未随正文提供，发布版不补造该图，改用公开假设的成本模型表。

## 阅读时的证据分级

- **官方文档可追溯：** 对应具体来源链接，可核对当时版本和开放范围。
- **厂商宣称：** 性能、规模、客户案例等，不视为独立实测。
- **原稿参考：** 保留原研究线索，但本次未逐项独立确认。
- **分析判断与建议：** 选型权衡、市场趋势和优先级，不冒充厂商事实或已落地结果。

原稿列出的 TechPlained、Upstash、Rajesh Beri 文章缺少具体 URL，因此未生成猜测链接。未来补充时应同时记录文章地址、访问日期、原始口径与一手出处。
