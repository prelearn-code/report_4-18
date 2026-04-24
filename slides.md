---
theme: seriph
title: Blockchain-Enabled Efficient Deduplication and Mixed Auditing for Dynamic Cloud Data
info: |
  IEEE Transactions on Dependable and Secure Computing
class: text-center
drawings:
  persist: false
transition: fade-out
mdc: true
hideInToc: true

---

## Blockchain-Enabled Efficient Deduplication and Mixed Auditing for Dynamic Cloud Data

<div class="pt-6 text-lg leading-8">

**Chunfei Pan（南京理工大学硕士）, Lei Zhou（南京理工大学博士）, Anmin Fu（南京理工大学教授 通讯）, Zhenzhu Chen（西南财经讲师）, Huaqun Wang（南京邮电教授）, Yifeng Zheng（港理工助理教授）, Yansong Gao（西澳大利亚大学讲师）**

</div>

<div class="pt-5 text-base leading-8">

**Journal:** IEEE Transactions on Dependable and Secure Computing (TDSC)  
**Received:** 11 September 2025  
**Accepted:** 23 November 2025  
**Published:** 27 November 2025  
**Current Version:** 12 March 2026

</div>

---
hideInToc: true
---

# 目录

<div class="max-w-[90%] mx-auto mt-8 grid grid-cols-2 gap-1 text-left text-[0.95rem] leading-7">

<div class="rounded-2xl border border-white/12 bg-white/5 px-6 py-5">
<div class="text-center text-blue-300 font-bold mb-2">Part 1</div>
<div class="text-center text-xl font-bold">研究背景与问题动机</div>
</div>

<div class="rounded-2xl border border-white/12 bg-white/5 px-6 py-5">
<div class="text-center text-green-300 font-bold mb-2">Part 2</div>
<div class="text-center text-xl font-bold">相关工作与本文定位</div>
</div>

<div class="rounded-2xl border border-white/12 bg-white/5 px-6 py-5">
<div class="text-center text-yellow-300 font-bold mb-2">Part 3</div>
<div class="text-center text-xl font-bold">系统模型与设计目标</div>
</div>

<div class="rounded-2xl border border-white/12 bg-white/5 px-6 py-5">
<div class="text-center text-red-300 font-bold mb-2">Part 4</div>
<div class="text-center text-xl font-bold">方案初始化与上传去重</div>
</div>

<div class="rounded-2xl border border-white/12 bg-white/5 px-6 py-5">
<div class="text-center text-cyan-300 font-bold mb-2">Part 5</div>
<div class="text-center text-xl font-bold">混合审计与数据检索</div>
</div>

<div class="rounded-2xl border border-white/12 bg-white/5 px-6 py-5">
<div class="text-center text-purple-300 font-bold mb-2">Part 6</div>
<div class="text-center text-xl font-bold">动态更新机制</div>
</div>

<div class="rounded-2xl border border-white/12 bg-white/5 px-6 py-5">
<div class="text-center text-pink-300 font-bold mb-2">Part 7</div>
<div class="text-center text-xl font-bold">所有权转移机制</div>
</div>

<div class="rounded-2xl border border-white/12 bg-white/5 px-6 py-5">
<div class="text-center text-orange-300 font-bold mb-2">Part 8</div>
<div class="text-center text-xl font-bold">实验评估与总结</div>
</div>

</div>

---
hideInToc: true
---

# Part 1 研究背景与问题动机

<div class="mt-10 text-left text-xl leading-10">

- 研究概述
- 研究背景
- 研究动机

</div>

---
title: 研究概述
---

<h1 class="text-center">研究概述</h1>

<div class="max-w-[90%] mx-auto">

<div class="mt-4 rounded-2xl border border-white/12 overflow-hidden">

<div class="text-center grid grid-cols-2 bg-white/6 text-[1.05rem] font-bold">
  <div class="px-5 py-3 border-r border-white/12">现有方案的核心问题</div>
  <div class="px-5 py-3">本文的对应思路</div>
</div>

<div class="grid grid-cols-2 border-t border-white/12 text-[0.82rem] leading-6">
  <div class="px-5 py-4 border-r border-white/12">
    <span class="text-center font-bold text-red-300">问题 1：</span>
    现有 <b>cross-user deduplication</b> 虽能减少存储，但与 <b>pay-as-you-go</b> 收费模式不协调，可能导致多用户为同一份数据重复付费。
  </div>
  <div class="px-5 py-4">
    <span class="text-center font-bold text-blue-300">思路 1：</span>
    采用<b>用户侧 deduplication</b>，在用户本地完成 file / block 级去重，不再强调跨用户共享同一物理副本。
  </div>
</div>

<div class="grid grid-cols-2 border-t border-white/12 text-[0.82rem] leading-6">
  <div class="px-5 py-4 border-r border-white/12">
    <span class="text-center font-bold text-red-300">问题 2：</span>
    多用户共享同一副本时，容易削弱<b>数据隔离</b>，同时也会增加后续管理与维护的复杂度。
  </div>
  <div class="px-5 py-4">
    <span class="text-center font-bold text-blue-300">思路 2：</span>
    设计<b>mixed plaintext-ciphertext auditing</b>，将 plaintext 与 ciphertext 混合存储和审计，在隐私保护与处理效率之间取得平衡。
  </div>
</div>

<div class="grid grid-cols-2 border-t border-white/12 text-[0.82rem] leading-6">
  <div class="px-5 py-4 border-r border-white/12">
    <span class="text-center font-bold text-red-300">问题 3：</span>
    单副本设计通常不利于<b>动态更新</b>和<b>所有权转移</b>，容易带来维护和归属上的问题。
  </div>
  <div class="px-5 py-4">
    <span class="text-center font-bold text-blue-300">思路 3：</span>
    借助<b>blockchain</b> 与 <b>smart contract</b>，把审计、动态数据操作和 <b>ownership transfer</b> 放到同一框架中统一处理。
  </div>
</div>

</div>

<div class="mt-4 text-[0.9rem] leading-6 opacity-90">
<b>核心结论：</b> 本文不是单独优化去重或审计，而是把 <b>去重、审计、动态更新、所有权转移</b> 四个问题统一起来一起解决。
</div>

</div>

<!--
思路2中的内容：就是为了后续统一进行审计，使用同一套审计体系。
-->

---
title: 研究背景
---

<h1 class="text-center">研究背景</h1>

<div class="max-w-[90%] mx-auto">

<div class="mt-4 rounded-2xl border border-white/12 overflow-hidden">

<div class="text-center grid grid-cols-2 bg-white/6 text-[1.05rem] font-bold">
  <div class="px-5 py-3 border-r border-white/12">云存储带来的现实变化</div>
  <div class="px-5 py-3">云存储面临的安全问题</div>
</div>

<div class="grid grid-cols-2 border-t border-white/12 text-[0.84rem] leading-6">
  <div class="px-5 py-4 border-r border-white/12">
    <span class="text-center font-bold text-blue-300">背景 1：</span>
    在大数据时代，越来越多用户将本地数据外包到云端，借助 CSP(Cloud Service Providers) 获得更强的存储能力与可扩展性。
  </div>
  <div class="px-5 py-4">
    <span class="text-center font-bold text-red-300">问题 1：</span>
    数据上传到云端后，用户通常不再长期保留完整本地副本，因此很难直接确认云端数据是否仍然完好。
  </div>
</div>

<div class="grid grid-cols-2 border-t border-white/12 text-[0.84rem] leading-6">
  <div class="px-5 py-4 border-r border-white/12">
    <span class="text-center font-bold text-blue-300">背景 2：</span>
    云服务通常采用 <b>pay-as-you-go</b> 模式，用户按照存储量和服务时长付费，云存储已经成为主流数据管理方式。
  </div>
  <div class="px-5 py-4">
    <span class="text-center font-bold text-red-300">问题 2：</span>
    即使 CSP 声称服务可靠，云环境中仍可能发生<b>数据丢失</b>、<b>数据损坏</b>或其他异常情况。
  </div>
</div>

<div class="grid grid-cols-2 border-t border-white/12 text-[0.84rem] leading-6">
  <div class="px-5 py-4 border-r border-white/12">
    <span class="text-center font-bold text-blue-300">背景 3：</span>
    用户希望把存储负担转移到云端，但同时也希望能够持续确认外包数据的真实状态。
  </div>
  <div class="px-5 py-4">
    <span class="text-center font-bold text-red-300">问题 3：</span>
    更严重的是，CSP 可能为了维护自身声誉而谎称数据仍然完整，因此需要一种可验证的 <b>integrity auditing</b> 机制。
  </div>
</div>

</div>

<div class="mt-4 rounded-xl border border-yellow-300/40 bg-yellow-300/8 px-5 py-3 text-[0.9rem] leading-6">
云存储提升了使用便利性，但也把“数据是否仍被正确保存”变成了一个必须单独解决的问题，这正是后续引入 <b>auditing</b> 机制的直接原因。
</div>

</div>

<!--
pag-as-you-go模式就是，存储使用多少的物理空间就支付多少的费用。
-->

---
title: 研究动机
---

<h1 class="text-center">研究动机</h1>

<div class="max-w-[90%] mx-auto">

<div class="mt-4 rounded-2xl border border-white/12 overflow-hidden">

<div class="text-center grid grid-cols-2 bg-white/6 text-[1.05rem] font-bold">
  <div class="px-5 py-3 border-r border-white/12">现有 deduplication 的局限</div>
  <div class="px-5 py-3">本文要进一步解决的问题</div>
</div>

<div class="grid grid-cols-2 border-t border-white/12 text-[0.84rem] leading-6">
  <div class="px-5 py-4 border-r border-white/12">
    <span class="text-center font-bold text-red-300">局限 1：</span>
    传统去重主要关注“减少重复存储”，但没有充分考虑云存储中的实际收费模式。
  </div>
  <div class="px-5 py-4">
    <span class="text-center font-bold text-blue-300">目标 1：</span>
    既要利用 deduplication 提升存储效率，又要避免与 <b>pay-as-you-go</b> 模式产生冲突。
  </div>
</div>

<div class="grid grid-cols-2 border-t border-white/12 text-[0.84rem] leading-6">
  <div class="px-5 py-4 border-r border-white/12">
    <span class="text-center font-bold text-red-300">局限 2：</span>
    多用户共享同一物理副本时，虽然节省空间，但会削弱<b>数据隔离</b>，也会增加后续管理复杂度。
  </div>
  <div class="px-5 py-4">
    <span class="text-center font-bold text-blue-300">目标 2：</span>
    在保持去重收益的同时，仍然让不同用户保有各自独立、可维护的数据副本关系。
  </div>
</div>

<div class="grid grid-cols-2 border-t border-white/12 text-[0.84rem] leading-6">
  <div class="px-5 py-4 border-r border-white/12">
    <span class="text-center font-bold text-red-300">局限 3：</span>
    单副本设计通常不利于<b>动态更新</b>和<b>所有权转移</b>，因为后续修改、交易和归属判断都会变得复杂。
  </div>
  <div class="px-5 py-4">
    <span class="text-center font-bold text-blue-300">目标 3：</span>
    让系统不仅能审计和去重，还能进一步支持<b>动态数据操作</b>与<b>ownership transfer</b>。
  </div>
</div>

</div>

<div class="mt-4 rounded-xl border border-yellow-300/40 bg-yellow-300/8 px-5 py-3 text-[0.9rem] leading-6">
本文的出发点不是简单追求“去重越多越好”，而是要在 <b>存储效率、收费合理性、数据隔离和后续可操作性</b> 之间找到更平衡的方案。
</div>

</div>
---
hideInToc: true
---

# Part 2 相关工作与本文定位

<div class="mt-10 text-left text-xl leading-10">

- 相关工作
- 现有工作的不足
- 本文的核心贡献

</div>

---
title: 相关工作
---

<h1 class="text-center">相关工作</h1>

<div class="max-w-[90%] mx-auto">

<div class="mt-4 rounded-2xl border border-white/12 overflow-hidden">

<div class="text-center grid grid-cols-3 bg-white/6 text-[1rem] font-bold">
  <div class="px-5 py-3 border-r border-white/12">研究路线 1</div>
  <div class="px-5 py-3 border-r border-white/12">研究路线 2</div>
  <div class="px-5 py-3">研究路线 3</div>
</div>

<div class="grid grid-cols-3 border-t border-white/12 text-[0.8rem] leading-6">
  <div class="px-5 py-4 border-r border-white/12">
    <div class="text-center font-bold text-blue-300 mb-2">Data Integrity Auditing</div>
   关注如何验证云端数据是否仍然完整； 典型思路是通过随机抽样、认证标签等方式避免下载全部数据；一部分工作进一步支持 <b>dynamic data</b> 操作
  </div>

  <div class="px-5 py-4 border-r border-white/12">
    <div class="text-center font-bold text-green-300 mb-2">Blockchain-Based Auditing</div>
    关注如何去掉对 <b>TPA（Third-Party Auditor）</b> 的依赖；主要借助 <b>blockchain</b> 的公开可验证性与不可篡改性  
    ；通过 <b>smart contract</b> 实现自动审计与结果记录
  </div>

  <div class="px-5 py-4">
    <div class="text-center font-bold text-yellow-300 mb-2">Deduplication + Auditing</div>
    关注如何把存储去重与完整性审计结合起来  ；目标是在节省存储空间的同时仍保持可验证性。
  </div>
</div>

</div>

<div class="mt-4 grid grid-cols-3 gap-4">

<div class="rounded-xl border border-blue-300/30 bg-blue-300/8 px-4 py-3 text-[0.82rem] leading-6">
<b>主线 1 的重点</b><br>
先解决“数据还在不在、对不对”的问题
</div>

<div class="rounded-xl border border-green-300/30 bg-green-300/8 px-4 py-3 text-[0.82rem] leading-6">
<b>主线 2 的重点</b><br>
再解决“谁来审计、如何避免过度信任”的问题
</div>

<div class="rounded-xl border border-yellow-300/30 bg-yellow-300/8 px-4 py-3 text-[0.82rem] leading-6">
<b>主线 3 的重点</b><br>
进一步解决“如何同时兼顾效率与可验证性”的问题
</div>

</div>

<div class="mt-4 rounded-xl border border-yellow-300/40 bg-yellow-300/8 px-5 py-3 text-[0.88rem] leading-6">
已有工作并不是在解决同一个层面的问题，而是分别围绕 <b>审计机制、信任模型、存储效率</b> 展开；本文的工作位于第三条主线，并进一步把动态更新和所有权转移也纳入进来。
</div>

</div>

<!--
本文的信任模型是半可信 CSP / 半可信卖方 + 区块链可信
-->

---
title: 现有工作的不足
---

<h1 class="text-center">现有工作的不足</h1>

<div class="max-w-[90%] mx-auto">

<div class="mt-4 rounded-2xl border border-white/12 overflow-hidden">

<div class="text-center grid grid-cols-2 bg-white/6 text-[1.05rem] font-bold">
  <div class="px-5 py-3 border-r border-white/12">已有方案已经做到的部分</div>
  <div class="px-5 py-3">仍然存在的关键不足</div>
</div>

<div class="grid grid-cols-2 border-t border-white/12 text-[0.84rem] leading-6">
  <div class="px-5 py-4 border-r border-white/12">
    <span class="text-center font-bold text-blue-300">已有进展 1：</span>
    一些方案已经支持 cloud data 的完整性审计，也有一部分工作利用 <b>blockchain</b> 和 <b>smart contract</b> 降低了对 <b>TPA</b> 的依赖。
  </div>
  <div class="px-5 py-4">
    <span class="text-center font-bold text-red-300">不足 1：</span>
    仍有方案在关键环节依赖第三方，或者虽然引入区块链，但带来了较高的链上计算、通信或交互开销。
  </div>
</div>

<div class="grid grid-cols-2 border-t border-white/12 text-[0.84rem] leading-6">
  <div class="px-5 py-4 border-r border-white/12">
    <span class="text-center font-bold text-blue-300">已有进展 2：</span>
    一些研究已经尝试把 <b>deduplication</b> 和 <b>auditing</b> 结合起来，以同时提升存储效率和可验证性。
  </div>
  <div class="px-5 py-4">
    <span class="text-center font-bold text-red-300">不足 2：</span>
    但不少方案主要面向单一功能点，往往只能支持 file-level 或 block-level 中的一部分能力，或者缺少对 mixed auditing 的支持。
  </div>
</div>

<div class="grid grid-cols-2 border-t border-white/12 text-[0.84rem] leading-6">
  <div class="px-5 py-4 border-r border-white/12">
    <span class="text-center font-bold text-blue-300">已有进展 3：</span>
    部分方案已经考虑了去重环境下的安全性与审计正确性，功能上比传统 auditing 更进一步。
  </div>
  <div class="px-5 py-4">
    <span class="text-center font-bold text-red-300">不足 3：</span>
    很少有方案能够同时支持 <b>mixed plaintext-ciphertext auditing</b>、<b>dynamic data operations</b> 和 <b>ownership transfer</b>，这也正是本文试图补上的部分。
  </div>
</div>

</div>

<div class="mt-4 grid grid-cols-3 gap-4">

<div class="text-center rounded-xl border border-blue-300/30 bg-blue-300/8 px-4 py-1 text-[0.82rem] leading-6">
<b>问题一</b><br>
功能往往分散，缺少统一框架
</div>

<div class=" text-center rounded-xl border border-green-300/30 bg-green-300/8 px-4 py-0 text-[0.82rem] leading-6">
<b>问题二</b><br>
去掉 TPA 后，链上或交互开销可能上升
</div>

<div class="rounded-xl border border-yellow-300/30 bg-yellow-300/8 px-4 py-1 text-[0.82rem] leading-6">
<b>问题三</b><br>
对更新与交易场景支持仍然不足
</div>

</div>

<div class="mt-4 rounded-xl border border-yellow-300/40 bg-yellow-300/8 px-5 py-3 text-[0.88rem] leading-6">
现有工作已经分别解决了审计、去信任化和去重中的部分问题，但还没有形成一个能够同时兼顾效率、隔离性、动态更新和所有权转移的完整方案。
</div>

</div>

<!--
但不少方案主要面向单一功能点，往往只能支持 file-level 或 block-level 中的一部分能力，或者缺少对 mixed auditing 的支持。
-->

---
title: 本文的核心贡献
---

<h1 class="text-center">本文的核心贡献</h1>

<div class="max-w-[90%] mx-auto">

<div class="mt-5 grid grid-cols-3 gap-5">

<div class="rounded-2xl border border-blue-300/30 bg-blue-300/8 px-5 py-5 text-[0.82rem] leading-6">
<div class="text-center text-[1rem] font-bold text-blue-300 mb-3">贡献一</div>

本文设计了一种新的 **HV(Homomorphic Verifiable Tree)** 架构，并将其与 **MLE(Message Locked Encryption)** 结合起来：
- 支持 **file-level deduplication**
- 支持 **block-level deduplication**
- 支持 **mixed plaintext-ciphertext auditing**
- 利用 **ECC** 加密数据密钥

</div>

<div class="rounded-2xl border border-green-300/30 bg-green-300/8 px-5 py-5 text-[0.82rem] leading-6">
<div class="text-center text-[1rem] font-bold text-green-300 mb-3">贡献二</div>

本文借助 **blockchain** 与 **smart contract** 进一步实现：

- 自动化的完整性审计
- 不依赖 **TPA** 的验证流程
- 对 **dynamic data operations** 的支持
- 安全的 **ownership transfer**

这样使方案更接近真实云存储场景。

</div>

<div class="rounded-2xl border border-yellow-300/30 bg-yellow-300/8 px-5 py-5 text-[0.82rem] leading-6">
<div class="text-center text-[1rem] font-bold text-yellow-300 mb-3">贡献三</div>

论文从两个方面验证了方案有效性：

- 给出了安全性分析与正确性证明
- 给出了与已有工作的实验对比
- 展示了较好的审计效率
- 尤其在 **data upload** 阶段具有明显优势

说明该方案不仅能做，而且做得相对高效。

</div>

</div>

<div class="mt-5 rounded-xl border border-yellow-300/40 bg-yellow-300/8 px-5 py-3 text-[0.88rem] leading-6">
本文的创新点不在单一模块，而在于把 <b>去重、混合审计、动态更新和所有权转移</b> 放进了同一个基于 blockchain 的统一框架中。
</div>

</div>

---
hideInToc: true
---

# Part 3 系统模型与设计目标

<div class="mt-10 text-left text-xl leading-10">

- 系统模型
- 设计目标
- 整体流程图
- 方案总览

</div>

---
title: 系统模型
---

<h1 class="text-center">系统模型</h1>

<div class="max-w-[90%] mx-auto">

<div class="mt-5 grid grid-cols-3 gap-5">

<div class="rounded-2xl border border-blue-300/30 bg-blue-300/8 px-5 py-5 text-[0.82rem] leading-6">
<div class="text-center text-[1rem] font-bold text-blue-300 mb-3">User</div>

- 用户本地存储能力有限，需要将数据外包到云端
- 在上传前完成数据处理，并发起去重、审计和更新请求
- 按照存储量与审计服务向系统支付相应费用
- 在需要时发起数据检索和所有权转移

</div>

<div class="rounded-2xl border border-green-300/30 bg-green-300/8 px-5 py-5 text-[0.82rem] leading-6">
<div class="text-center text-[1rem] font-bold text-green-300 mb-3">CSP</div>

- 提供云端存储与计算资源
- 负责执行数据存储、去重和完整性证明生成
- 在方案中参与 file / block 级去重处理
- 但也可能为了维护声誉而伪造证明或隐瞒数据异常

</div>

<div class="rounded-2xl border border-yellow-300/30 bg-yellow-300/8 px-5 py-5 text-[0.82rem] leading-6">
<div class="text-center text-[1rem] font-bold text-yellow-300 mb-3">Blockchain</div>

- 负责记录存储元数据、审计日志和交易信息
- 依靠不可篡改特性提供公开可验证的记录
- 通过 <b>smart contract</b> 自动发起和验证审计
- 同时承担费用结算、押金约束和交易仲裁功能

</div>

</div>

<div class="mt-5 rounded-2xl border border-white/12 overflow-hidden">

<div class="text-center grid grid-cols-4 bg-white/6 text-[0.92rem] font-bold">
  <div class="px-4 py-3 border-r border-white/12">上传阶段</div>
  <div class="px-4 py-3 border-r border-white/12">审计阶段</div>
  <div class="px-4 py-3 border-r border-white/12">更新阶段</div>
  <div class="px-4 py-3">交易阶段</div>
</div>

<div class="grid grid-cols-4 border-t border-white/12 text-[0.8rem] leading-6">
  <div class="px-4 py-3 border-r border-white/12">
    User 先发起去重检查，随后将唯一数据上传给 CSP，并把费用信息提交到链上
  </div>
  <div class="px-4 py-3 border-r border-white/12">
    User 发起审计请求，<b>smart contract</b> 生成 challenge，CSP 返回 proof
  </div>
  <div class="px-4 py-3 border-r border-white/12">
    User 提交修改、插入或删除请求，CSP 执行更新并把验证信息写入链上
  </div>
  <div class="px-4 py-3">
    两个用户通过链上合约完成付款、押金约束和 <b>ownership transfer</b>
  </div>
</div>

</div>

</div>

<!--
半信任模型
-->

---
title: 设计目标
---

<h1 class="text-center text-[2rem] leading-tight">设计目标</h1>

<div class="max-w-[90%] mx-auto mt-5 grid grid-cols-3 gap-5">

<div class="rounded-2xl border border-blue-300/30 bg-blue-300/8 px-4 py-4 text-[0.74rem] leading-6">
  <div class="text-center text-[0.9rem] font-bold text-blue-300 mb-2">目标一 · Automatic Auditing</div>
  <ul class="list-disc pl-5 space-y-1">
    <li>借助 <b>smart contract</b> 自动发起并验证审计流程</li>
    <li>不再依赖传统 <b>TPA</b></li>
    <li>使审计结果能够被链上公开记录与验证</li>
  </ul>
</div>

<div class="rounded-2xl border border-green-300/30 bg-green-300/8 px-4 py-4 text-[0.74rem] leading-6">
  <div class="text-center text-[0.9rem] font-bold text-green-300 mb-2">目标二 · User-Side Deduplication</div>
  <ul class="list-disc pl-5 space-y-1">
    <li>在用户侧支持 <b>file-level</b> 与 <b>block-level deduplication</b></li>
    <li>减少重复数据与重复认证器带来的开销</li>
    <li>避免 cross-user 去重带来的收费与隔离问题</li>
  </ul>
</div>

<div class="rounded-2xl border border-yellow-300/30 bg-yellow-300/8 px-4 py-4 text-[0.74rem] leading-6">
  <div class="text-center text-[0.9rem] font-bold text-yellow-300 mb-2">目标三 · Mixed Auditing</div>
  <ul class="list-disc pl-5 space-y-1">
    <li>支持 <b>plaintext</b> 与 <b>ciphertext</b> 混合审计</li>
    <li>不要求整份文件全部加密</li>
    <li>在隐私保护与处理效率之间取得平衡</li>
  </ul>
</div>

<div class="rounded-2xl border border-cyan-300/30 bg-cyan-300/8 px-4 py-4 text-[0.74rem] leading-6">
  <div class="text-center text-[0.9rem] font-bold text-cyan-300 mb-2">目标四 · Data Dynamics</div>
  <ul class="list-disc pl-5 space-y-1">
    <li>支持数据块的<b>修改、插入、删除</b></li>
    <li>使云端存储不只是“存进去”，还能持续维护</li>
    <li>满足更接近真实场景的使用需求</li>
  </ul>
</div>

<div class="rounded-2xl border border-purple-300/30 bg-purple-300/8 px-4 py-4 text-[0.74rem] leading-6">
  <div class="text-center text-[0.9rem] font-bold text-purple-300 mb-2">目标五 · Ownership Transfer</div>
  <ul class="list-disc pl-5 space-y-1">
    <li>支持云端数据的<b>所有权转移</b></li>
    <li>通过链上合约完成费用约束与交易确认</li>
    <li>使数据交易后的访问控制更清晰</li>
  </ul>
</div>

<div class="rounded-2xl border border-pink-300/30 bg-pink-300/8 px-4 py-4 text-[0.74rem] leading-6">
  <div class="text-center text-[0.9rem] font-bold text-pink-300 mb-2">目标六 · Access Control</div>
  <ul class="list-disc pl-5 space-y-1">
    <li>通过身份验证机制防止未授权访问</li>
    <li>限制非法修改与越权检索</li>
    <li>保证后续更新和交易过程中的身份合法性</li>
  </ul>
</div>

</div>

---
title: 整体流程图
---

<h1 class="text-center text-[2rem] leading-tight">整体流程图</h1>

<div class="max-w-[90%] mx-auto mt-5 flex justify-center">
  <img
    src="/images/整体工作流图片.png"
    class="w-[78%] max-h-[68vh] object-contain rounded-xl bg-white p-2"
  />
</div>

---
title: 方案总览
---

<h1 class="text-center text-[2rem] leading-tight">方案总览</h1>

<div class="max-w-[90%] mx-auto mt-5 rounded-2xl border border-white/12 overflow-hidden">

<div class="text-center grid grid-cols-4 bg-white/6 text-[0.95rem] font-bold">
  <div class="px-4 py-3 border-r border-white/12">阶段一</div>
  <div class="px-4 py-3 border-r border-white/12">阶段二</div>
  <div class="px-4 py-3 border-r border-white/12">阶段三</div>
  <div class="px-4 py-3">阶段四</div>
</div>

<div class="grid grid-cols-4 border-t border-white/12 text-[0.78rem] leading-6">
  <div class="px-4 py-4 border-r border-white/12">
    <div class="text-center font-bold text-blue-300 mb-2">上传与去重</div>
    <ul class="list-disc pl-5 space-y-1">
      <li>User 先对文件进行预处理</li>
      <li>向 CSP 发起 duplicate checking</li>
      <li>仅上传 unique data blocks 与相关认证信息</li>
    </ul>
  </div>

  <div class="px-4 py-4 border-r border-white/12">
    <div class="text-center font-bold text-green-300 mb-2">链上审计</div>
    <ul class="list-disc pl-5 space-y-1">
      <li>User 发起 audit request</li>
      <li><b>smart contract</b> 生成 challenge</li>
      <li>CSP 返回 proof，链上自动验证结果</li>
    </ul>
  </div>

  <div class="px-4 py-4 border-r border-white/12">
    <div class="text-center font-bold text-yellow-300 mb-2">动态更新</div>
    <ul class="list-disc pl-5 space-y-1">
      <li>支持修改、插入、删除等操作</li>
      <li>CSP 执行更新并重构验证结构</li>
      <li>更新结果继续写入 blockchain</li>
    </ul>
  </div>

  <div class="px-4 py-4">
    <div class="text-center font-bold text-pink-300 mb-2">所有权转移</div>
    <ul class="list-disc pl-5 space-y-1">
      <li>两个用户通过链上合约发起交易</li>
      <li>完成费用支付、押金约束与身份确认</li>
      <li>最终实现 <b>ownership transfer</b></li>
    </ul>
  </div>
</div>

</div>

<div class="max-w-[90%] mx-auto mt-5 grid grid-cols-4 gap-4">

<div class="rounded-xl border border-blue-300/30 bg-blue-300/8 px-4 py-3 text-[0.78rem] leading-6">
<b>核心输入</b><br>
原始文件、用户身份信息、密钥与标签
</div>

<div class="rounded-xl border border-green-300/30 bg-green-300/8 px-4 py-3 text-[0.78rem] leading-6">
<b>核心机制</b><br>
用户侧 deduplication + mixed auditing
</div>

<div class="rounded-xl border border-yellow-300/30 bg-yellow-300/8 px-4 py-3 text-[0.78rem] leading-6">
<b>可信支撑</b><br>
blockchain + smart contract + 链上记录
</div>

<div class="rounded-xl border border-pink-300/30 bg-pink-300/8 px-4 py-3 text-[0.78rem] leading-6">
<b>核心输出</b><br>
可审计、可更新、可交易的云端存储状态
</div>

</div>

---
hideInToc: true
---

# Part 4 方案初始化与上传去重

<div class="max-w-[90%] mx-auto mt-8 text-left text-[1.05rem] leading-9">

- 系统初始化
- 核心函数
- 上传与去重机制（一）：数据预处理与文件表示
- 上传与去重机制（二）：密钥生成与标签构造
- 上传与去重机制（三）：身份认证与去重检查
- 上传与去重机制（四）：唯一块上传与存储落链

</div>

---
title: 系统初始化
---

<h1 class="text-center text-[2rem] leading-tight">系统初始化</h1>

<div class="max-w-[90%] mx-auto mt-5 grid grid-cols-2 gap-5">

::CardBox
<div class="text-center text-[1rem] font-bold text-blue-300 mb-3">初始化函数：Setup</div>

- 输入安全参数 `λ`，生成公共参数集合 `para`
- 选择两个阶为 $p$ 的双线性群 $G_1$ 和 $G_2$
- 构造双线性映射 $e: G_1 \times G_1 \rightarrow G_2$
- 选取生成元 $g \in G_1$ 与随机元素集合 $R = \{r_j\}$
::

::CardBox
<div class="text-center text-[1rem] font-bold text-green-300 mb-3">初始化结果</div>

- 定义哈希函数 $H_1$、$H_2$、$H_3$、$H_4$
- 定义伪随机置换 $f_1$ 与伪随机函数 $f_2$
- 这些参数会被上传、审计、更新与交易模块共同调用

$$
\mathrm{para} = \{G_1, G_2, p, e, g, R, H_1, H_2, H_3, H_4, f_1, f_2\}
$$
::
</div>

<div class="max-w-[90%] mx-auto mt-4 grid grid-cols-4 gap-3">

::CardBox
<div class="text-center font-bold text-yellow-300 mb-2">群参数</div>

$$
G_1, G_2, p, e, g
$$
::

::CardBox
<div class="text-center font-bold text-cyan-300 mb-2">随机元素</div>

$$
R = \{r_j\}
$$
::

::CardBox
<div class="text-center font-bold text-lime-300 mb-2">哈希函数</div>

$$
H_1, H_2, H_3, H_4
$$
::

::CardBox
<div class="text-center font-bold text-pink-300 mb-2">伪随机工具</div>

$$
f_1, f_2
$$
::

</div>


---
title: 核心函数
---

<h1 class="text-center text-[2rem] leading-tight">核心函数</h1>

<div class="max-w-[90%] mx-auto mt-5 grid grid-cols-2 gap-5">
<div class="rounded-2xl border border-blue-300/30 bg-blue-300/8 px-5 py-5 text-[0.8rem] leading-7">
<div class="text-center text-[1rem] font-bold text-blue-300 mb-3">函数集合</div>
<ul class="list-disc pl-5 space-y-2">
<li><b>上传相关：</b>KeyGen、Encrypt、TagGen、AuthGen</li>
<li><b>审计相关：</b>AuditReq、ProofGen、VerifyProof</li>
<li><b>恢复相关：</b>Decrypt</li>
<li><b>动态更新相关：</b>Modify、Insert、Delete</li>
</ul>
</div>

<div class="rounded-2xl border border-green-300/30 bg-green-300/8 px-5 py-5 text-[0.8rem] leading-7">
<div class="text-center text-[1rem] font-bold text-green-300 mb-3">模块调用关系</div>
<ul class="list-disc pl-5 space-y-2">
<li>KeyGen 到 AuthGen：负责把数据处理后上传</li>
<li>AuditReq 到 VerifyProof：负责生成并验证审计证据</li>
<li>Decrypt：负责数据恢复</li>
<li>Modify、Insert、Delete：负责维护动态数据状态</li>
</ul>
</div>
</div>

<div class="max-w-[90%] mx-auto mt-5 grid grid-cols-3 gap-4">
<div class="text-center rounded-xl border border-yellow-300/30 bg-yellow-300/8 px-4 py-3 text-[0.76rem] leading-6">
<div class="text-center font-bold text-yellow-300 mb-2">上传阶段</div>
KeyGen<br>
Encrypt<br>
TagGen<br>
AuthGen
</div>

<div class="text-center rounded-xl border border-cyan-300/30 bg-cyan-300/8 px-4 py-3 text-[0.76rem] leading-6">
<div class="text-center font-bold text-cyan-300 mb-2">审计阶段</div>
AuditReq<br>
ProofGen<br>
VerifyProof
</div>

<div class="text-center rounded-xl border border-pink-300/30 bg-pink-300/8 px-4 py-3 text-[0.76rem] leading-6">
<div class="text-center font-bold text-pink-300 mb-2">动态维护阶段</div>
Modify<br>
Insert<br>
Delete
</div>
</div>

---
title: 上传与去重机制（一）
---

<h1 class="text-center text-[2rem] leading-tight">上传与去重机制（一）：数据预处理与文件表示</h1>

<div class="max-w-[90%] mx-auto mt-5 grid grid-cols-2 gap-5">

::CardBox
<div class="text-center text-[1rem] font-bold text-blue-300 mb-3">步骤 1：文件划分与数据组织</div>

- 用户首先将原始文件 $F$ 划分为 $n$ 个等长数据块
- 每个数据块再进一步划分为 $s$ 个 sector，得到更细粒度的数据表示
- 如果最后一个 block 长度不足，则在末尾补零，保证后续处理结构一致
- 最终，文件可表示为 $F = \{m_{i,j}\}$，其中 $i$ 表示 block 编号，$j$ 表示 sector 编号
::

::CardBox
<div class="text-center text-[1rem] font-bold text-green-300 mb-3">步骤 2：公开数据与私密数据分离</div>

- 文件被进一步划分为两部分：$F_1$ 和 $F_2$
- $F_1$ 表示公开可用的数据块，后续保持明文形式
- $F_2$ 表示包含敏感信息的数据块，后续进入加密流程
- 因此，系统同时保存 `plaintext` 与 `ciphertext`，这也是后面 `mixed auditing` 的基础
::

</div>

<div class="max-w-[90%] mx-auto mt-5 grid grid-cols-3 gap-4">

::CardBox
<div class="text-center font-bold text-yellow-300 mb-2">文件级表示</div>

$$F = F_1 \cup F_2$$

公开数据与私密数据先分离，再分别处理。
::

::CardBox
<div class="text-center font-bold text-cyan-300 mb-2">块级表示</div>

$$F = \{m_i\}$$

每个 $m_i$ 对应一个数据块。
::

::CardBox
<div class="text-center font-bold text-pink-300 mb-2">sector 级表示</div>

$$F = \{m_{i,j}\}$$

每个 block 再细分为多个 sector。
::

</div>

---
title: 上传与去重机制（二）
---

<h1 class="text-center text-[2rem] leading-tight">上传与去重机制（二）：密钥生成与标签构造</h1>

<div class="max-w-[90%] mx-auto mt-5">

<div class="grid grid-cols-2 gap-5">

::CardBox
<div class="text-center text-[1rem] font-bold text-blue-300 mb-3">步骤 3：密钥生成与私密块加密</div>

- 系统先根据整个文件生成文件密钥 $fk = H_1(F)$
- 再根据每个 sector 生成对应的 sector key $k_{i,j} = H_1(m_{i,j})$
- 对私密数据块中的敏感 sector 执行加密，公开数据块 $F_1$ 保持明文
- 这样就形成了 plaintext 与 ciphertext 并存的数据结构

$$
c^{c}_{i,j} = H_3(k^{c}_{i,j}) \oplus m^{c}_{i,j}
$$
::

::CardBox
<div class="text-center text-[1rem] font-bold text-green-300 mb-3">步骤 4：标签构造与认证准备</div>

- 处理完成后，系统得到统一的数据块集合 $C=\{c_i\}$
- 文件标签写成 $t = g^{fk}$，用于文件级标识
- 块标签写成 $tg_i = H_1(c_i)$，用于 block-level deduplication
- 这些标签后续会继续参与 duplicate checking 和 authenticator 生成
- 因此，这一步把原始文件转成了可去重、可审计的结构化表示
::

</div>

<div class="grid grid-cols-3 gap-3 mt-3">

::CardBox
<div class="text-center font-bold text-yellow-300 mb-1">文件密钥</div>

$$fk = H_1(F)$$
由整个文件生成，用于构造文件级标签。
::

::CardBox
<div class="text-center font-bold text-cyan-300 mb-1">sector key</div>

$$k_{i,j} = H_1(m_{i,j})$$
由每个 sector 单独生成，用于私密数据加密。
::

::CardBox
<div class="text-center font-bold text-pink-300 mb-1">块标签</div>

$$
tg_i = H_1(c_i)
$$
后续用于去重检查与认证器构造。
::

</div>

</div>

---
title: 上传与去重机制（三）
---

<h1 class="text-center text-[2rem] leading-tight">上传与去重机制（三）：身份认证与去重检查</h1>

<div class="max-w-[90%] mx-auto mt-5">

<div class="grid grid-cols-2 gap-4">

::CardBox
<div class="text-center text-[0.96rem] font-bold text-blue-300 mb-3">步骤 5：身份绑定与认证请求</div>

- 先认证身份，再进行 deduplication
- 用户选取 $\mu \in \mathbb{Z}_p^{*}$，将 $\mathit{uid}$ 与文件标签 $t$ 绑定
- 向 CSP 发送 $\langle t,\; T,\; \{Key_i\},\; \mathit{uid},\; UID,\; W \rangle$

$$
UID = \bigl(H_4(\mathit{uid}) \cdot t\bigr)^{\mu}
$$

$$
W = g^{\mu}
$$
::

::CardBox
<div class="text-center text-[0.96rem] font-bold text-green-300 mb-3">步骤 6：CSP 先验身份，再做两级去重</div>

- 先验证身份合法性
- 再执行 file-level 与 block-level deduplication
- 若 $t$ 已存在，则整文件重复
- 否则由 $T=\{tg_i\}$ 找到唯一块标签集合 $T_u$

$$
e(UID, g) \stackrel{?}{=} e\bigl(H_4(\mathit{uid}) \cdot t,\; W\bigr)
$$
::

</div>

<div class="grid grid-cols-3 gap-3 mt-3">

::CardBox
<div class="text-center font-bold text-yellow-300 mb-2">唯一块参数</div>

$$
y_i = \left( \sum_{j=1}^{s} k_{i,j} \right) \oplus \gamma,\\
\qquad
\gamma \in \mathbb{Z}_p^{*}
$$

$$
Y_i = g^{y_i}
$$
::

::CardBox
<div class="text-center font-bold text-cyan-300 mb-2">authenticator</div>

$$
\sigma_i =
\left(
H_2\bigl(s \parallel tg_i\bigr)
\cdot
\prod_{j=1}^{s} r_j^{\,c_{i,j}}
\right)^{y_i}
$$
::

::CardBox
<div class="text-center font-bold text-pink-300 mb-2">一致性验证</div>

$$
e(\sigma_i, g)
\stackrel{?}{=}\\
e\!\left(
H_2\bigl(s \parallel tg_i\bigr)
\cdot
\prod_{j=1}^{s} r_j^{\,c_{i,j}},
\; Y_i
\right)
$$
::

</div>

</div>

<!--
$\mu$ 比较像用户的私钥参数
T:标识区块标签集合
-->

---
title: 上传与去重机制（四）
---

<h1 class="text-center text-[1.7rem] leading-tight">上传与去重机制（四）：唯一块上传与存储落链</h1>

<div class="max-w-[90%] mx-auto mt-3">

<div class="grid grid-cols-2 gap-3">

::CardBox
<div class="text-center text-[0.9rem] font-bold text-blue-300 mb-2">步骤 7：唯一块上传与本地保留信息</div>

- 用户仅上传唯一块集合 $C_u$ 与对应认证器
- CSP 验证通过后，保存标签、密钥密文与唯一块信息
- 用户本地删除原文件，仅保留最小访问信息

$$
\langle C_u,\; \sigma=\{\sigma_i\} \rangle
$$

$$
\langle t,\; T,\; \{Key_i\},\; T_u,\; C_u \rangle
$$

$$
\langle t,\; sk \rangle
$$
::

::CardBox
<div class="text-center text-[0.9rem] font-bold text-green-300 mb-2">步骤 8：构造HVT</div>

- 叶子节点保存块标签
- 内部节点由左右孩子哈希聚合得到
- 根节点 $w_r$ 作为后续更新与审计的状态摘要

$$
h_i = tg_i
$$

$$
h = H_1\!\bigl(h_{l\mathrm{children}} \parallel h_{r\mathrm{children}}\bigr)
$$

$$
l_N = l_{l\mathrm{children}} + l_{r\mathrm{children}}
$$
::

</div>

<div class="grid grid-cols-3 gap-2 mt-3 px-1">

::CardBox
<div class="text-center font-bold text-yellow-300 mb-1">节点三元组</div>

$$
(h,\; l_N,\; p)
$$

$$
p_{\mathrm{root}} = 0
$$
::

::CardBox
<div class="text-center font-bold text-cyan-300 mb-1">链上存储信息</div>

$$
Info =
\langle
t,\; T_u,\; \sigma,\; uid,\; SID,\; w_r
\rangle
$$
::

::CardBox
<div class="text-center font-bold text-pink-300 mb-1">保证金</div>

$$
Fee_1 = 2\,fee_1
$$
::

</div>

</div>

<!--
三元组，h:标识哈希 l_N:当前节点下面有多少个可访问叶子节点 p:当前节点在本层的编号
SID:标识存储这个数据的CSP

保证金是CSP发送的两倍保证金，后续验证有问题的话，就会把这个保证金全给用户。
-->

---
hideInToc: true
---

# Part 5 混合审计与数据检索

<div class="max-w-[90%] mx-auto mt-8 text-left text-[1.05rem] leading-9">

- 混合审计机制（一）：审计请求与挑战生成
- 混合审计机制（二）：证明生成与聚合结果
- 混合审计机制（三）：证明验证与审计结果
- 数据检索机制：身份复验与数据恢复

</div>

---
title: 混合审计机制（一）
---

<h1 class="text-center text-[1.7rem] leading-tight">混合审计机制（一）：审计请求与挑战生成</h1>

<div class="max-w-[90%] mx-auto mt-4">

<div class="grid grid-cols-2 gap-4">

::CardBox
<div class="text-center text-[0.9rem] font-bold text-blue-300 mb-2">步骤 1：用户发起审计请求</div>

- 用户向 smart contract 提交审计请求 $req$
- 同时预存审计费用 $fee_2$
- 之后由链上合约自动触发 challenge 生成

$$
AuditReq(req) \rightarrow Chal
$$

$$
fee_2
$$
::

::CardBox
<div class="text-center text-[0.9rem] font-bold text-green-300 mb-2">步骤 2：合约生成挑战</div>

- smart contract 自动生成挑战元组
- 其中 $z$ 表示挑战块数量
- $\theta_1,\theta_2$ 用于后续导出索引与权重

$$
Chal = (z,\; \theta_1,\; \theta_2)
$$

$$
z \in [1,n], \qquad \theta_1,\theta_2 \in \mathbb{Z}_p^{*}
$$
::

</div>

<div class="grid grid-cols-2 gap-4 mt-3 px-4">

::CardBox
<div class="text-center font-bold text-yellow-300 mb-1">挑战索引生成</div>

$$
x_i = f_1(i,\theta_1)
$$

$$
Q = \{x_i\}_{i=1}^{z}
$$
::

::CardBox
<div class="text-center font-bold text-pink-300 mb-1">挑战权重生成</div>

$$
v_i = f_2(i,\theta_2)
$$

$$
\{v_i\}_{i=1}^{z}
$$
::

</div>

</div>

---
title: 混合审计机制（二）
---

<h1 class="text-center text-[1.7rem] leading-tight">混合审计机制（二）：证明生成与聚合结果</h1>

<div class="max-w-[90%] mx-auto mt-4">

<div class="grid grid-cols-2 gap-4">

::CardBox
<div class="text-center text-[0.9rem] font-bold text-blue-300 mb-2">步骤 3：CSP 根据挑战定位被审计块</div>

- CSP 从链上读取挑战 $Chal=(z,\theta_1,\theta_2)$
- 根据伪随机函数确定被挑战块索引与对应权重
- 挑战块集合记为 $Q=\{x_i\}_{i=1}^{z}$

$$
x_i = f_1(i,\theta_1)
$$

$$
v_i = f_2(i,\theta_2)
$$
::

::CardBox
<div class="text-center text-[0.9rem] font-bold text-green-300 mb-2">步骤 4：按 sector 聚合生成审计证明</div>

- 对每个 sector $j$，把所有被挑战块的对应内容加权求和
- 这里统一使用处理后的块内容 $c_{x_i,j}$
- 因此 plaintext 与 ciphertext 都进入同一证明计算过程

$$
P_j = \sum_{i=1}^{z} v_i\, c_{x_i,j}
$$

$$
P = \{P_j\}_{j=1}^{s}
$$
::

</div>

<div class="grid grid-cols-3 gap-3 mt-2 px-2">

::CardBox
<div class="text-center font-bold text-yellow-300 mb-1">挑战输入</div>

$$
Chal = (z,\theta_1,\theta_2)
$$
::

::CardBox
<div class="text-center font-bold text-cyan-300 mb-1">证明向量</div>

$$
P = \{P_1,P_2,\dots,P_s\}
$$
::

::CardBox
<div class="text-center font-bold text-pink-300 mb-1">单个分量</div>

$$
P_j = \sum_{i=1}^{z} v_i\, c_{x_i,j}
$$
::

</div>

</div>

---
title: 混合审计机制（三）
---

<h1 class="text-center text-[1.7rem] leading-tight">混合审计机制（三）：证明验证与审计结果</h1>

<div class="max-w-[90%] mx-auto mt-4">

<div class="grid grid-cols-2 gap-4">

::CardBox
<div class="text-center text-[0.9rem] font-bold text-blue-300 mb-2">步骤 5：聚合认证器生成</div>

- smart contract 根据挑战块对应认证器生成聚合结果
- 聚合认证器 $\sigma_c$ 作为后续验证输入

$$
\sigma_c = \prod_{i=1}^{z} \sigma_{x_i}^{\,v_i}
$$
::

::CardBox
<div class="text-center text-[0.9rem] font-bold text-green-300 mb-2">步骤 6：链上执行证明验证</div>

- smart contract 自动执行 VerifyProof
- 若下式成立，则说明 CSP 通过审计

$$
e(\sigma_c, g)
\stackrel{?}{=}
e\!\left(
\prod_{i=1}^{z} H_2\bigl(s \parallel tg_{x_i}\bigr)^{v_i}
\cdot
\prod_{j=1}^{s} r_j^{\,P_j},
\;
\prod_{i=1}^{z} Y_{x_i}
\right)
$$
::

</div>

<div class="grid grid-cols-2 gap-4 mt-3 px-4">

::CardBox
<div class="text-center font-bold text-yellow-300 mb-1">链上记录结果</div>

$$
\langle \sigma_c,\; P,\; result \rangle
$$

$$
result \in \{0,1\}
$$
::

::CardBox
<div class="text-center font-bold text-pink-300 mb-1">费用结算规则</div>

$$
result = 1 \;\Rightarrow\; fee_2 \to CSP
$$

$$
result = 0 \;\Rightarrow\; Fee_1 \to U
$$
::

</div>

</div>

---
title: 数据检索机制
---

<h1 class="text-center text-[1.7rem] leading-tight">数据检索机制：身份复验与数据恢复</h1>

<div class="max-w-[90%] mx-auto mt-4">

<div class="grid grid-cols-2 gap-4">

::CardBox
<div class="text-center text-[0.9rem] font-bold text-blue-300 mb-2">步骤 1：用户发起数据检索请求</div>

- 用户向 CSP 提交检索请求
- CSP 先验证当前访问者身份是否合法
- 只有认证通过后，才返回对应外包数据

$$
\langle t,\; UID,\; W \rangle
$$

$$
e(UID, g) \stackrel{?}{=} e\bigl(H_4(uid)\cdot t,\; W\bigr)
$$
::

::CardBox
<div class="text-center text-[0.9rem] font-bold text-green-300 mb-2">步骤 2：返回数据与密钥密文</div>

- CSP 返回处理后的数据集合与密钥密文
- 用户对公开数据直接读取
- 对私密数据，先恢复 sector key，再恢复明文内容

$$
\langle C,\; \{Key_i\} \rangle
$$

$$
K\text{-}Decrypt(sk,\; Key_i) \rightarrow \{k_{i,j}\}
$$
::

</div>

<div class="grid grid-cols-2 gap-4 mt-3 px-4">

::CardBox
<div class="text-center font-bold text-yellow-300 mb-1">私密 sector 解密</div>

$$
m^{c}_{i,j} = H_3\!\bigl(k^{c}_{i,j}\bigr) \oplus c^{c}_{i,j}
$$
::

::CardBox
<div class="text-center font-bold text-pink-300 mb-1">文件恢复结果</div>

$$
F = F_1 \cup F_2
$$

$$
F_2 = \{m^{c}_{i,j}\}
$$
::

</div>

</div>

<!--
t:标识文件标签
-->

---
hideInToc: true
---

# Part 6 动态更新机制

<div class="max-w-[90%] mx-auto mt-8 text-left text-[1.05rem] leading-9">

- 动态更新机制（一）：插入请求与唯一块认证
- 动态更新机制（二）：插入执行、MHT 更新与上链确认
- 动态更新机制（三）：批量插入与其他更新操作

</div>

---
title: 动态更新机制（一）
---

<h1 class="text-center text-[1.4rem] leading-tight">动态更新机制（一）：插入请求与唯一块认证</h1>

<div class="max-w-[90%] mx-auto mt-2">

<div class="grid grid-cols-2 gap-3">

::CardBox
<div class="text-center text-[0.86rem] font-bold text-blue-300 mb-1">步骤 1：用户发起插入请求</div>

<div class="text-[0.82rem] leading-6">

- 用户在第 $i$ 个位置后插入新块 $m^{*}$
- 私密块先加密，公开块直接保留明文
- 计算新块标签后，发送初始插入请求

</div>

$$
\begin{aligned}
k^{*}_{j} &= H_1(m^{*}_{j}) \\
c^{*}_{j} &= H_3(k^{*}_{j}) \oplus m^{*}_{j} \\
tg^{*} &= H_1(c^{*})
\end{aligned}
$$

$$
\langle Insert,\; UID,\; W,\; t,\; i,\; tg^{*} \rangle
$$
::

::CardBox
<div class="text-center text-[0.86rem] font-bold text-green-300 mb-1">步骤 2：CSP 认证身份并执行去重检查</div>

<div class="text-[0.82rem] leading-6">

- CSP 先验证用户身份
- 认证通过后，对待插入块执行重复检查
- 若为唯一块，则进入新块认证器生成阶段

</div>

$$
e(UID, g) \stackrel{?}{=} e\bigl(H_4(uid)\cdot t,\; W\bigr)
$$
::

</div>

<div class="mt-1">
<div class="scale-[0.9] origin-top">

<div class="grid grid-cols-2 gap-2 px-1">

::CardBox
<div class="text-center font-bold text-yellow-300 mb-0 text-[0.86rem]">新块参数生成</div>

$$
\begin{aligned}
y^{*} &= \left( \sum_{j=1}^{s} k^{*}_{j} \right) \oplus \gamma \\
Y^{*} &= g^{y^{*}}
\end{aligned}
$$
::

::CardBox
<div class="text-center font-bold text-pink-300 mb-0 text-[0.86rem]">新块认证器</div>

$$
\sigma^{*}
=
\left(
H_2\bigl(s \parallel tg^{*}\bigr)
\cdot
\prod_{j=1}^{s} r_j^{\,c^{*}_{j}}
\right)^{y^{*}}
$$

$$
\langle Insert,\; c^{*},\; \sigma^{*} \rangle
$$
::

</div>

</div>
</div>

</div>



---
title: 动态更新机制（二）
---

<h1 class="text-center text-[1.4rem] leading-tight">动态更新机制（二）：插入执行、MHT 更新与上链确认</h1>

<div class="max-w-[90%] mx-auto mt-2">

<div class="grid grid-cols-2 gap-3">

::CardBox
<div class="text-center text-[0.86rem] font-bold text-blue-300 mb-2">步骤 3：CSP 执行插入并更新存储状态</div>

<div class="text-[0.82rem] leading-6">

- CSP 接收最终插入请求 $\langle Insert,\; c^{*},\; \sigma^{*} \rangle$
- 存储新块，并在位置 $i$ 后插入新的叶子节点
- 随后更新对应块标签与根节点状态

</div>

$$
h^{*} = tg^{*}
$$

$$
\langle Insert,\; c^{*},\; \sigma^{*} \rangle
$$

$$
w_r \longrightarrow w_r^{*}
$$
::

::CardBox
<div class="text-center text-[0.86rem] font-bold text-green-300 mb-2">步骤 4：MHT 重计算与链上提交</div>

<div class="text-[0.82rem] leading-6">

- 插入后，自底向上重计算受影响路径
- 得到更新后的根节点 $w_r^{*}$
- CSP 将更新结果提交给 blockchain，供后续验证

</div>

$$
h = H_1\!\bigl(h_{l\mathrm{children}} \parallel h_{r\mathrm{children}}\bigr)
$$

$$
\langle t^{*},\; tg^{*},\; \sigma^{*},\; uid,\; SID,\; w_r^{*} \rangle
$$
::

</div>

<div class="grid grid-cols-1 gap-3 mt-2 px-2">

::CardBox
<div class="text-center font-bold text-yellow-300 mb-1 text-[0.82rem]">更新结果</div>

$$
Insert(Insert,\; t,\; i,\; tg^{*},\; c^{*}) \rightarrow w_r^{*}
$$
::

</div>

</div>

---
title: 动态更新机制（三）
---

<h1 class="text-center text-[1.4rem] leading-tight">动态更新机制（三）：批量插入与其他更新操作</h1>

<div class="max-w-[90%] mx-auto mt-2">

<div class="grid grid-cols-2 gap-3">

::CardBox
<div class="text-center text-[0.86rem] font-bold text-blue-300 mb-2">批量插入：用户侧处理</div>

<div class="text-[0.82rem] leading-6">

- 用户对批量插入块 $\{m^{*}_{j}\}_{j=1}^{\eta}$ 逐块处理
- 私密块加密后得到处理块集合 $\{c^{*}_{j}\}$
- 再计算对应标签集合 $\{tg^{*}_{j}\}$ 并发送批量请求

</div>

$$
\{m^{*}_{j}\}_{j=1}^{\eta}
\longrightarrow
\{c^{*}_{j}\}_{j=1}^{\eta}
$$

$$
tg^{*}_{j} = H_1(c^{*}_{j})
$$

$$
\bigl\{ \sigma^{*}_{j} \bigr\}_{j=1}^{\eta}
$$
::

::CardBox
<div class="text-center text-[0.86rem] font-bold text-green-300 mb-2">批量插入：CSP 执行与链上记录</div>

<div class="text-[0.82rem] leading-6">

- CSP 认证身份并完成 deduplication 检查
- 对非重复块执行批量插入并更新 MHT
- 最终把新根节点与相关元数据提交到 blockchain

</div>

$$
w_r \longrightarrow w_r^{*}
$$

$$
\left\langle
t^{*},\; \{tg^{*}_{j}\},\; \{\sigma^{*}_{j}\},\; uid,\; SID,\; w_r^{*}
\right\rangle
$$
::

</div>

<div class="grid grid-cols-2 gap-3 mt-2 px-2">

::CardBox
<div class="text-center font-bold text-yellow-300 mb-1 text-[0.82rem]">修改操作</div>

$$
Modify(Modify,\; t,\; i,\; tg^{*}_{i},\; c^{*}_{i})
\rightarrow
w_r^{*}
$$
::

::CardBox
<div class="text-center font-bold text-pink-300 mb-1 text-[0.82rem]">删除操作</div>

$$
Delete(Delete,\; t,\; i)
\rightarrow
w_r^{*}
$$
::

</div>

</div>

---
hideInToc: true
---

# Part 7 所有权转移机制

<div class="max-w-[90%] mx-auto mt-8 text-left text-[1.05rem] leading-9">

- 所有权转移机制（一）：交易发起、身份确认与所有者变更
- 所有权转移机制（二）：密钥交付、新拥有者访问结算

</div>

---
title: 所有权转移机制（一）
---

<h1 class="text-center text-[1.28rem] leading-tight">所有权转移机制（一）：交易发起、身份确认与所有者变更</h1>

<div class="max-w-[90%] mx-auto mt-1">

<div class="grid grid-cols-2 gap-2">

::CardBox
<div class="text-center text-[0.82rem] font-bold text-blue-300 mb-1">步骤 1：买方发起交易请求</div>

<div class="text-[0.78rem] leading-5">

- 数据购买者 $U_2$ 向 smart contract 提交所有权转移请求
- 请求中包含原拥有者与新拥有者身份
- 同时预存数据购买费用 $fee_3$

</div>

$$
\langle uid_1,\; uid_2 \rangle
$$

$$
fee_3
$$
::

::CardBox
<div class="text-center text-[0.82rem] font-bold text-green-300 mb-1">步骤 2：原拥有者提交身份信息并触发所有者更新</div>

<div class="text-[0.78rem] leading-5">

- 原拥有者 $U_1$ 向合约提交身份认证信息与文件标签
- 同时预存保证金 $Fee_3 = 2\,fee_3$
- 合约将完整交易信息发送给 CSP，触发云端所有者记录更新

</div>

$$
UID_1 = \bigl(H_4(uid_1)\cdot t\bigr)^{\mu_1}
$$

$$
W_1 = g^{\mu_1}
$$

$$
\langle UID_1,\; W_1,\; t \rangle
$$
::

</div>

<div class="mt-3">
<div class="scale-[0.8] origin-top">

<div class="grid grid-cols-2 gap-2 px-0">

::CardBox
<div class="text-center font-bold text-yellow-300 mb-0 text-[0.82rem]">CSP 身份验证</div>

$$
e(UID_1, g) \stackrel{?}{=} e\bigl(H_4(uid_1)\cdot t,\; W_1\bigr)
$$
::

::CardBox
<div class="text-center font-bold text-pink-300 mb-0 text-[0.82rem]">更新后链上记录</div>

$$
\langle t,\; T_u,\; uid_2,\; SID,\; w_r \rangle
$$

$$
Fee_3 = 2\,fee_3
$$
::

</div>

</div>
</div>

</div>

---
title: 所有权转移机制（二）
---

<h1 class="text-center text-[1.4rem] leading-tight">所有权转移机制（二）：密钥交付、新拥有者访问结算</h1>

<div class="max-w-[90%] mx-auto mt-2">

<div class="grid grid-cols-2 gap-3">

::CardBox
<div class="text-center text-[0.86rem] font-bold text-blue-300 mb-2">步骤 3：原拥有者交付密钥并接收交易费用</div>

<div class="text-[0.82rem] leading-6">

- 所有者更新完成后，$U_1$ 通过安全信道向 $U_2$ 发送解密密钥 $sk$
- smart contract 将买方预存的交易费用 $fee_3$ 转给 $U_1$
- 后续是否退还保证金，由 $U_2$ 的解密结果决定

</div>

$$
sk
$$

$$
fee_3 \rightarrow U_1
$$
::

::CardBox
<div class="text-center text-[0.86rem] font-bold text-green-300 mb-2">步骤 4：新拥有者发起访问并验证密钥正确性</div>

<div class="text-[0.82rem] leading-6">

- $U_2$ 基于新的身份信息向 CSP 发起数据访问请求
- CSP 按更新后的拥有者记录验证身份
- 若返回数据可被 $sk$ 正确解密，则说明转移成功

</div>

$$
UID_2 = \bigl(H_4(uid_2)\cdot t\bigr)^{\mu_2}
$$

$$
W_2 = g^{\mu_2}
$$

$$
\langle UID_2,\; W_2,\; t \rangle
$$
::

</div>

<div class="grid grid-cols-2 gap-3 mt-1 px-2">

::CardBox
<div class="text-center font-bold text-yellow-300 mb-0 text-[0.82rem]">身份验证与解密判定</div>

$$
e(UID_2, g) \stackrel{?}{=} e\bigl(H_4(uid_2)\cdot t,\; W_2\bigr)
$$

$$
m^{c}_{i,j} = H_3\!\bigl(k^{c}_{i,j}\bigr) \oplus c^{c}_{i,j}
$$
::

::CardBox
<div class="text-center font-bold text-pink-300 mb-0 text-[0.82rem]">结算结果</div>

$$
\text{success} \;\Rightarrow\; Fee_3 \rightarrow U_1
$$

$$
\text{failure} \;\Rightarrow\; Fee_3 \rightarrow U_2
$$
::

</div>

</div>

---
hideInToc: true
---

# Part 8 实验评估与总结

<div class="max-w-[90%] mx-auto mt-7 text-left text-[0.95rem] leading-8">

- 实验评估（一）：评估思路与实验设置
- 实验评估（二）：上传与审计计算开销对比
- 实验评估（三）：加密、解密与动态更新开销对比
- 实验评估（四）：通信开销对比
- 实验评估（五）：文件级去重方案对比
- 实验评估（六）：链上审计的 Gas 开销对比
- 实验评估（七）：所有权转移的 Gas 开销
- 实验评估（八）：实验结果总结
- 本文总结与展望

</div>

---
title: 实验评估（一）
---

<h1 class="text-center text-[1.4rem] leading-tight">实验评估（一）：评估思路与实验设置</h1>

<div class="max-w-[90%] mx-auto mt-2">

<div class="grid grid-cols-2 gap-3">

::CardBox
<div class="text-center text-[0.86rem] font-bold text-blue-300 mb-2">对比对象与评估内容</div>

<div class="text-[0.82rem] leading-6">

- 论文将本文方案与文献 [9]、[34]、[35] 进行主要对比
- 对仅支持 file-level deduplication 的文献 [10]，单独做文件级对比
- 评估内容包括 computation、communication、storage 与 gas cost

</div>

$$
\{[9],\; [34],\; [35]\}
$$

$$
\text{Computation} + \text{Communication} + \text{Storage} + \text{Gas}
$$
::

::CardBox
<div class="text-center text-[0.86rem] font-bold text-green-300 mb-2">实验平台与实现环境</div>

<div class="text-[0.82rem] leading-6">

- 链下实验环境为 Ubuntu 24.04.1 LTS
- 使用 Python 调用 PBC Library 与 GMP Library 实现密码计算
- 链上实验使用 Solidity 开发，并通过 Ganache 模拟私有链环境

</div>

$$
\text{Ubuntu 24.04.1 LTS}
$$

$$
\text{Python} + \text{PBC} + \text{GMP}
$$

$$
\text{Solidity} + \text{Ganache}
$$
::

</div>

<div class="grid grid-cols-2 gap-3 mt-2 px-2">

::CardBox
<div class="text-center font-bold text-yellow-300 mb-1 text-[0.82rem]">链下实验参数</div>

$$
|F|/n = 4\text{KiB};
s = 128
;D = 75\%
$$
::

::CardBox
<div class="text-center font-bold text-pink-300 mb-1 text-[0.82rem]">密码与统计设置</div>

$$
|G| = 512\ \text{bits}
;

;
|Z_p^{*}| = 160\ \text{bits}
;


1000\ \text{runs}
$$
::

</div>

</div>

---
title: 实验评估（二）
---

<h1 class="text-center text-[1.4rem] leading-tight">实验评估（二）：上传与审计计算开销对比</h1>

<div class="max-w-[90%] mx-auto mt-2">

<div class="grid grid-cols-2 gap-3">

::CardBox
<div class="text-center text-[0.86rem] font-bold text-blue-300 mb-2">图示结果</div>

<div class="text-[0.82rem] leading-6">

- 本页展示上传与审计阶段的 computation cost 对比
- 包括 tag generation、prove 与 verify 三部分
- 横轴对应数据块数量或挑战块数量，纵轴对应时间开销

</div>

<div class="mt-2 flex justify-center">
  <img
    src="/images/upload_audit.png"
    class="w-[100%] max-h-[50vh] object-contain rounded-lg bg-white p-1"
  />
</div>
::

::CardBox
<div class="text-center text-[0.86rem] font-bold text-green-300 mb-2">结果解读</div>

<div class="text-[0.82rem] leading-6">

- 在 tag generation 阶段，本文方案开销最低
- 原因是本文只对 unique block 生成 authenticator，而不是对全部块都生成
- 在 prove 阶段，本文方案也优于 [34]、[35]，与 [9] 接近
- 在 verify 阶段，本文方案与 [9] 基本接近，但明显优于 [35]

</div>

$$
\text{TagGen: our scheme} < [9], [34], [35]
$$

$$
\text{Prove: our scheme} \approx [9] < [35] < [34]
$$

$$
\text{Verify: our scheme} \approx [9] < [35]
$$
::

</div>

<div class="grid grid-cols-2 gap-3 mt-2 px-2">

::CardBox
<div class="text-center font-bold text-yellow-300 mb-1 text-[0.82rem]">优势来源</div>

$$
\text{deduplication before authenticator generation}
$$
::

::CardBox
<div class="text-center font-bold text-pink-300 mb-1 text-[0.82rem]">核心结论</div>

$$
\text{上传阶段优势最明显}
$$
::

</div>

</div>

---
title: 实验评估（三）
---

<h1 class="text-center text-[1.4rem] leading-tight">实验评估（三）：加密、解密与动态更新开销对比</h1>

<div class="max-w-[90%] mx-auto mt-2">

<div class="grid grid-cols-2 gap-3">

::CardBox
<div class="text-center text-[0.86rem] font-bold text-blue-300 mb-2">图示结果</div>

<div class="text-[0.82rem] leading-6">

- 本页展示 encrypt、decrypt 与 update 三部分的 computation cost 对比
- 其中加密与解密部分重点考察私密数据占比变化带来的影响
- update 部分展示本文方案支持动态更新时的额外开销

</div>

<div class="mt-2 flex justify-center">
  <img
    src="/images/encrypt_decrypt_update.png"
    class="w-[92%] max-h-[44vh] object-contain rounded-lg bg-white p-1"
  />
</div>
::

::CardBox
<div class="text-center text-[0.86rem] font-bold text-green-300 mb-2">结果解读</div>

<div class="text-[0.82rem] leading-6">

- 本文方案只对私密 sector 加密，因此私密数据占比越低，计算开销越小
- 在 encrypt 阶段，本文方案明显优于 [34]、[35]，但略高于 [9]
- 在 decrypt 阶段，当私密数据比例接近 $100\%$ 时，本文方案开销才逐渐接近其他方案
- 此外，本文方案额外支持 dynamic update，实验中插入 $1000$ 个数据块时开销仍处于可接受范围

</div>

$$
\omega = \frac{n-\zeta}{n};
\omega \downarrow \;\Rightarrow\; \text{Encrypt/Decrypt Cost} \downarrow
;\\
1000\ \text{blocks update} \approx 2.78\,s
$$
::

</div>

<div class="grid grid-cols-2 gap-3 mt-2 px-2">

::CardBox
<div class="text-center font-bold text-yellow-300 mb-1 text-[0.82rem]">优势来源</div>

$$
\text{only partial private data are encrypted}
$$
::

::CardBox
<div class="text-center font-bold text-pink-300 mb-1 text-[0.82rem]">核心结论</div>

$$
\text{私密数据越少，本文方案越有优势}
$$
::

</div>

</div>

---
title: 实验评估（四）
---

<h1 class="text-center text-[1.4rem] leading-tight">实验评估（四）：通信开销对比</h1>

<div class="max-w-[90%] mx-auto mt-2">

<div class="grid grid-cols-2 gap-3">

::CardBox
<div class="text-center text-[0.86rem] font-bold text-blue-300 mb-2">图示结果</div>

<div class="text-[0.82rem] leading-6">

- 本页展示 upload 与 auditing 两阶段的 communication cost 对比
- 重点比较本文方案与 [9]、[34]、[35] 在传输开销上的差异
- 其中 upload 反映上传阶段通信代价，auditing 反映审计阶段证明传输代价

</div>

<div class="mt-2 flex justify-center">
  <img
    src="/images/communication_cost.png"
    class="w-[92%] max-h-[44vh] object-contain rounded-lg bg-white p-1"
  />
</div>
::

::CardBox
<div class="text-center text-[0.86rem] font-bold text-green-300 mb-2">结果解读</div>

<div class="text-[0.82rem] leading-6">

- 在 upload 阶段，[34] 的通信开销明显更大，因为需要传输额外辅助信息
- 本文方案虽然还需上传处理后的密钥信息，但总体通信开销仍与 [9] 接近
- 在 auditing 阶段，本文方案、[9] 与 [34] 都明显优于 [35]
- 这是因为本文方案的审计证明规模主要与 sector 数 $s$ 有关，而与挑战块数 $z$ 无关

</div>

$$
\text{Upload: } [34] > \text{our scheme} \approx [9];\qquad|P| \propto s
$$
$$
\text{Auditing: } [35] > \text{our scheme} \approx [9];\qquad |P| \not\propto z
$$

::

</div>

<div class="grid grid-cols-2 gap-3 mt-2 px-2">

::CardBox
<div class="text-center font-bold text-yellow-300 mb-1 text-[0.82rem]">优势来源</div>

$$
\text{proof size depends on } s \text{ rather than } z
$$
::

::CardBox
<div class="text-center font-bold text-pink-300 mb-1 text-[0.82rem]">核心结论</div>

$$
\text{本文方案在通信开销上保持较好平衡}
$$
::

</div>

</div>

---
title: 实验评估（五）
---

<h1 class="text-center text-[1.4rem] leading-tight">实验评估（五）：文件级去重方案对比</h1>

<div class="max-w-[90%] mx-auto mt-2">

<div class="grid grid-cols-2 gap-3">

::CardBox
<div class="text-center text-[0.86rem] font-bold text-blue-300 mb-2">图示结果</div>

<div class="text-[0.82rem] leading-6">

- 本页对本文方案与仅支持 file-level deduplication 的 [10] 进行单独比较
- 对比内容包括 file tag generation、prove、verify 与 encrypt 四部分

</div>

<div class="mt-2 flex justify-center">
  <img
    src="/images/file_level_dedup.png"
    class="w-[65%] max-h-[35vh] object-contain rounded-lg bg-white p-1"
  />
</div>
::

::CardBox
<div class="text-center text-[0.86rem] font-bold text-green-300 mb-2">结果解读</div>

<div class="text-[0.82rem] leading-6">

- 两种方案在 file tag generation 阶段开销相同，均约为 $0.0008\,s$
- 在 prove 阶段，[10] 需要计算聚合认证器，因此开销更高
- 在 verify 阶段，本文方案略高于 [10]，因为聚合验证主要放在链上完成
- 在 encrypt 阶段，本文方案略高，但换来了更细粒度的隐私保护能力

</div>

$$
\text{File TagGen} \approx 0.0008\,s;
\text{Prove: our scheme} < [10]
$$

$$
\text{Verify: our scheme} > [10]
$$
::

</div>

<div class="grid grid-cols-2 gap-3 mt-1 px-2">

::CardBox
<div class="text-center font-bold text-yellow-300 mb-1 text-[0.82rem]">实验设置</div>

$$
|F| = 2000 \times 4\text{KiB}
;
\omega = 50\%, \qquad z = 460
$$
::

::CardBox
<div class="text-center font-bold text-pink-300 mb-0 text-[0.82rem]">核心结论</div>

$$
\text{本文方案在文件级场景下仍保持可接受开销，}\\
{并提供更强的块级隐私保护能力。}
$$
::

</div>

</div>


---
title: 实验评估（六）
---

<h1 class="text-center text-[1.4rem] leading-tight">实验评估（六）：链上审计的 Gas 开销对比</h1>

<div class="max-w-[90%] mx-auto mt-2">

<div class="grid grid-cols-2 gap-3">

::CardBox
<div class="text-center text-[0.86rem] font-bold text-blue-300 mb-2">图示结果</div>

<div class="text-[0.82rem] leading-6">

- 本页展示 data auditing 阶段的链上 gas cost 对比
- 对比对象仍为本文方案与 [9]、[34]、[35]
- 主要比较 Challenge、Prove 与 Verify 三个阶段的链上开销

</div>

<div class="mt-2 flex justify-center">
  <img
    src="/images/gas_auditing.png"
    class="w-[80%] max-h-[44vh] object-contain rounded-lg bg-white p-1"
  />
</div>
::

::CardBox
<div class="text-center text-[0.86rem] font-bold text-green-300 mb-2">结果解读</div>

<div class="text-[0.82rem] leading-6">

- 在 Challenge 与 Prove 阶段，本文方案 gas 略高
- 主要原因是本文在链上还处理了审计费用与保证金逻辑
- 在 Verify 阶段，本文方案与 [9]、[34] 同属 smart contract 验证模式
- 虽然存在一定链上成本，但换来了自动审计与对不诚实 CSP 的惩罚能力

</div>

$$
\text{Challenge} \approx 3.90 \times 10^{5}
$$

$$
\text{Prove} \approx 1.83 \times 10^{5}
$$

$$
\text{Verify} \approx 2.35 \times 10^{6}
$$
::

</div>

<div class="grid grid-cols-2 gap-3 mt-2 px-2">

::CardBox
<div class="text-center font-bold text-yellow-300 mb-1 text-[0.82rem]">优势来源</div>

$$
\text{smart contract} + \text{penalty mechanism}
$$
::

::CardBox
<div class="text-center font-bold text-pink-300 mb-1 text-[0.82rem]">核心结论</div>

$$
\text{适度链上成本换来更强的自动审计保障}
$$
::

</div>

</div>

---
title: 实验评估（七）
---

<h1 class="text-center text-[1.4rem] leading-tight">实验评估（七）：所有权转移的 Gas 开销</h1>

<div class="max-w-[90%] mx-auto mt-2">

<div class="grid grid-cols-2 gap-3">

::CardBox
<div class="text-center text-[0.86rem] font-bold text-blue-300 mb-2">图示结果</div>

<div class="text-[0.82rem] leading-6">

- 本页展示 data ownership transaction 各阶段的链上 gas cost
- 对应流程包括买方发起请求、卖方提交身份信息、CSP 返回更新结果以及买方反馈交易结果

</div>

<div class="mt-2 flex justify-center">
  <img
    src="/images/gas_ownership_transfer.png"
    class="w-[85%] max-h-[44vh] object-contain rounded-lg bg-white p-1"
  />
</div>
::

::CardBox
<div class="text-center text-[0.86rem] font-bold text-green-300 mb-2">结果解读</div>

<div class="text-[0.82rem] leading-6">

- $U_2$ 发起所有权转移请求时，需要上传身份信息并预付交易费用
- $U_1$ 提交身份验证信息和保证金，链上继续推进交易流程
- CSP 更新云端拥有者记录后，把结果回传给 smart contract
- 最后由 $U_2$ 反馈交易结果，合约依据结果退还或转移保证金

</div>

$$
1.48 \times 10^{5};
1.43 \times 10^{5}
$$

$$
1.37 \times 10^{5};
0.48 \times 10^{5}
$$
::

</div>

<div class="grid grid-cols-2 gap-3 mt-2 px-2">

::CardBox
<div class="text-center font-bold text-yellow-300 mb-1 text-[0.82rem]">开销特征</div>

$$
\text{Gas cost is independent of file block number}
$$
::

::CardBox
<div class="text-center font-bold text-pink-300 mb-1 text-[0.82rem]">核心结论</div>

$$
\text{ownership transfer 的链上开销总体可接受}
$$
::

</div>

</div>

---
title: 实验评估（八）
---

<h1 class="text-center text-[1.4rem] leading-tight">实验评估（八）：实验结果总结</h1>

<div class="max-w-[90%] mx-auto mt-2">

<div class="grid grid-cols-2 gap-3">

::CardBox
<div class="text-center text-[0.86rem] font-bold text-blue-300 mb-2">链下实验总结</div>

<div class="text-[0.82rem] leading-6">

- 在上传阶段，本文方案的优势最明显
- 在 tag generation 与 authenticator generation 阶段，本文方案整体开销最低
- 在 prove 与 verify 阶段，本文方案保持与现有高效方案相近的性能
- 当私密数据占比较低时，本文方案在 encrypt 与 decrypt 阶段优势更加突出

</div>

$$
\text{Upload Cost: our scheme is the lowest}
$$

$$
\omega \downarrow \;\Rightarrow\; \text{Encrypt/Decrypt Cost} \downarrow
$$
::

::CardBox
<div class="text-center text-[0.86rem] font-bold text-green-300 mb-2">链上实验总结</div>

<div class="text-[0.82rem] leading-6">

- 本文方案在 auditing 与 ownership transfer 阶段都引入了链上开销
- 虽然 gas cost 有所增加，但同时获得了自动审计、押金约束与结果仲裁能力
- ownership transfer 的链上开销不依赖文件块数量，因而具有较好的可扩展性
- 从整体看，链上代价与获得的安全能力是匹配的

</div>

$$
\text{Gas Cost} \uparrow \;\Rightarrow\; \text{Automation and Penalty} \uparrow
$$

$$
\text{Ownership Transfer Cost} \not\propto n
$$
::

</div>

<div class="grid grid-cols-2 gap-3 mt-2 px-2">

::CardBox
<div class="text-center font-bold text-yellow-300 mb-1 text-[0.82rem]">综合优势</div>

$$
\text{Efficiency} + \text{Mixed Auditing} + \text{Dynamics} + \text{Transfer}
$$
::

::CardBox
<div class="text-center font-bold text-pink-300 mb-1 text-[0.82rem]">实验结论</div>

$$
\text{本文方案在功能完整性与性能之间取得了较好平衡}
$$
::

</div>

</div>

---
title: 本文总结与展望
---

<h1 class="text-center text-[1.4rem] leading-tight">本文总结与展望</h1>

<div class="max-w-[90%] mx-auto mt-2">

<div class="grid grid-cols-2 gap-3">

::CardBox
<div class="text-[0.86rem] font-bold text-blue-300 mb-2">工作总结</div>

<div class="text-[0.82rem] leading-6">

- 本文面向云存储场景，统一考虑了 deduplication、mixed auditing、dynamic data 与 ownership transfer
- 方案在用户侧完成 file-level 与 block-level deduplication，避免 cross-user 去重带来的收费与隔离问题
- 通过 blockchain 与 smart contract，实现了自动审计、结果记录与押金约束
- 通过增强型 MHT 与身份认证机制，进一步支持动态更新和安全交易

</div>

::

::CardBox
<div class="text-center text-[0.86rem] font-bold text-green-300 mb-2">论文结论</div>

<div class="text-[0.82rem] leading-6">

- 理论分析说明方案满足正确性、安全性与机密性要求
- 实验结果表明，本文方案在上传阶段优势尤其明显
- 当私密数据比例较低时，部分加密带来的效率优势更加突出
- 整体上，本文在功能完整性、实用性与性能之间取得了较好平衡

</div>

$$
\text{Security} + \text{Efficiency} + \text{Practicality}
$$
::

</div>

<div class="grid grid-cols-2 gap-3 mt-2 px-2">

::CardBox
<div class="font-bold text-yellow-300 mb-1 text-[0.82rem]">未来工作</div>

$$
\text{Multi-Cloud Environment}
$$

$$
\text{Distributed Systems}
$$
::

::CardBox
<div class="font-bold text-pink-300 mb-1 text-[0.82rem]">进一步方向</div>

$$
\text{Stronger Compatibility}
$$

$$
\text{Resistance to Quantum Attacks}
$$
::

</div>

</div>
