# V2X Message Processing — Engineering Case Study

车联网消息处理与离线解码验证项目的技术说明草稿。仅包含案例文档，不包含原始研究数据、生产配置、第三方 JAR 或未确认授权的源码。

## Implementation context

The inspected Java/Maven project contains MQTT sources/sinks, Apache Flink processing dependencies, and entry points for BSM, MAP, SPAT, RSM and RSI messages. A separate offline validation directory investigates packet framing and ASN.1 decoding compatibility.

## Technical story

Incoming packets → transport framing → decoding → typed message processing → configured sinks. Offline validation checks framing and semantic output independently of live transport.

The existing audit notes identify a framing issue: trimming a packet using received length minus one can remove a payload byte. The documented alternative uses the declared body length after validating framing. The audit compares semantic output rather than only checking whether decoding returns an object.

This case study is based on local code and existing notes. No throughput, accuracy or end-to-end reproducibility claim is made; results were not rerun during portfolio preparation.

## Limitations

- Runtime/schema dependencies include generated ASN.1 classes and an external decoder runtime.
- Existing notes describe unresolved MAP compatibility differences and incomplete RSM sample validation.
- Original source contains database configuration and credential-related connection code.
- Code ownership, data publication rights and decoder redistribution permission are not established by local files.

## Before releasing source

1. Identify personal contributions and third-party/organisational components.
2. Confirm publication permission.
3. Replace embedded connection settings with local configuration and credential-free examples.
4. Provide synthetic redistributable fixtures and schema/runtime prerequisites.
5. Re-run offline validation and publish reproducible, authorised results.

## Interview presentation

Explain the processing pipeline, successful parsing versus correct semantics, and how offline fixtures isolate decoder problems from transport problems. State your actual contribution.

Suggested repository name after clearance: v2x-message-validation.
