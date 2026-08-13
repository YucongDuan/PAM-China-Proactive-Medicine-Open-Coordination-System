# PAM-China 中国主动医学开放协同系统

**PAM-China Proactive Medicine Open Coordination System**  
**版本：1.0.0 · DIKWP MESH8.1 · Apache-2.0**

PAM-China 是一个面向中国医院、基层医疗卫生机构、家庭医生团队、基本公共卫生、县域医共体、城市医疗集团和区域全民健康平台的主动医学开源参考实现。它把居民健康意图、主动发现、人工解释、目标共创、协同任务、连续监测、结局复核和开放残差组织为可运行闭环，同时提供 FHIR R4、HL7 v2/MLLP、CDA R2、DICOMweb 与厂商 REST 的接口暂存层。

本项目不是“自动诊断系统”。它的核心是：

- 让居民目的、来源、责任主体、同意与失效边界始终可见；
- 让医院、基层、公卫、康复、中医和区域平台在同一任务链上协同；
- 让每个健康信号只触发问题队列、人工复核或协同任务；
- 让服务包、字段映射、接口消息、证据来源和结局口径全部版本化、可审计、可撤销；
- 让 D/I/K/W/P 五元语义在正向生成与反向重建中保留差异与残差。

> **重要边界**：发行包只含合成数据和接口沙箱，不包含真实患者数据、生产端点、账号、证书、密钥、电子签名或外部写回授权。系统不自动诊断、开方、调整治疗、合并患者、确认号源床位，也不替代急诊、执业人员、医院制度、伦理审查或监管批准。

## 1. 直接运行

要求：Python 3.10 或更高版本。完整演示不需要 `pip install`。

### Windows

双击：

```text
打开PAM-China主动医学系统.bat
```

### macOS / Linux

```bash
chmod +x START_DEMO.command START_DEMO.sh
./START_DEMO.sh
```

### 通用命令

```bash
python start_showcase.py
```

浏览器打开 `http://127.0.0.1:8788`。

演示账号：

| 用户名 | 工作流角色 | 主要范围 |
|---|---|---|
| `doctor` | 临床责任角色 | 临床复核、服务包确认、方案、转衔 |
| `gp` | 家庭医生 | 主动发现、签约随访、目标与任务协调 |
| `public` | 公共卫生 | 重点人群、筛查、免疫和健康促进协同 |
| `nurse` | 护理 | 观察、随访、转衔和任务执行 |
| `tcm` | 中医临床 | 中医治未病与临床责任记录 |
| `rehab` | 康复治疗 | 康复目标、任务和连续记录 |
| `quality` | 质量安全 | 审计、复核与质量改进 |
| `research` | 科研观察 | 去标识只读与证据观察 |
| `resident` | 居民代理 | 健康意图、自我记录和打卡 |
| `admin` | 管理员 | 演示环境全部能力 |

默认密码：`mesh81-demo`。这些角色只是演示工作流标签，不构成真实身份、执业资格或电子签名。

## 2. 无 Python 离线展示

双击：

```text
PAM-China_主动医学离线展示_双击打开.html
```

离线版内嵌合成数据、样式与交互，不启动数据库和接口服务。

## 3. 关键运行模块

1. **区域运营总览**：人群覆盖、开放信号、服务包在管关系、接口暂存和跨层级责任通道。
2. **人群运营**：九条全生命周期合成人群旅程、服务覆盖、开放问题和任务分层。
3. **主动信号中心**：明确优先人工复核、资料来源缺口和连续随访开放状态。
4. **居民全景**：原始意图、同意、责任团队、服务包、目标、任务、观察和转衔。
5. **服务包注册中心**：15 个健康中国行动工程映射包与 9 个实施扩展包。
6. **协同任务**：家庭医生、医院、公卫、护理、康复、中医和居民共同在环。
7. **健康信息互联**：FHIR、HL7、CDA、DICOMweb、REST、MPI、暂存、队列和审计。
8. **证据与结局**：来源、版本、适用范围、失效边界和多维结局口径。
9. **MESH8.1**：D/I/K/W/P 五元位置、25 条有向路径、正反向连续性与残差。
10. **治理与审计**：用途、同意、最小权限、保守身份匹配、可靠重放和追加式审计。
11. **落地架构**：从单点试点到医院—基层—医共体—区域平台的部署蓝图。

## 4. 服务包目录

`data/domain_packs.json` 含 24 个可治理服务包：

- `hc-01` 至 `hc-15`：健康知识、营养、健身、控烟、心理、环境、妇幼、学校、职业、老年、心脑血管、癌症、呼吸、糖尿病、传染病与免疫等工程映射；
- `impl-16` 至 `impl-24`：家庭医生主动随访、筛查与免疫、多病共管、用药核对、出院转衔、康复、中医治未病、支持照护、真实世界证据与质量改进。

这些服务包是工程工作流容器，不是官方临床路径或自治医疗规则。机构必须依据本地规范、伦理、资质、术语和证据完成二次审核。

## 5. 互联接口

主要端点：

```text
GET  /api/health
POST /api/auth/login
GET  /api/showcase/bootstrap
GET  /api/showcase/population
GET  /api/showcase/evidence
GET  /api/cases/{case_id}
GET  /api/cases/{case_id}/mesh81
GET  /api/integration/dashboard
GET  /api/integration/connectors
GET  /api/integration/messages
POST /api/integration/fhir
POST /api/integration/hl7
POST /api/integration/cda
POST /api/integration/webhook
GET  /fhir/R4/metadata
GET  /dicomweb/studies
```

所有外部数据默认经过：

```text
接收 → 安全验证 → 身份候选/核验 → 映射版本 → 语义残差
→ 用途与权限检查 → 临床暂存 → 人工批准/驳回/补充
```

启用可选本地 MLLP：

```bash
python start_showcase.py --mllp-host 127.0.0.1 --mllp-port 2575
```

## 6. 生产部署原则

建议按以下路径实施：

```text
只读目录与临床暂存
→ 患者/就诊身份核验
→ LIS/PACS/转诊状态联调
→ 字段、代码集和单位校准
→ SIT
→ UAT 与人因验证
→ 安全、隐私、审计和恢复验收
→ 低风险状态回传
→ 经专项审批后再考虑高影响写回
```

生产必须替换演示令牌和密码，并通过医院 IAM/OIDC、mTLS、密钥管理、可信时间、电子签名、主数据、术语服务、数据库、高可用、监控、备份和灾备体系接管。

## 7. 工程命令

```bash
python run.py catalog
python run.py demo --kind cardio --out outputs/cardio
python run.py analyze data/demo_cardio.json --out outputs/analyzed.json
python run.py verify-audit
python run.py test
python tools/qa_summary.py
```

Docker 配置已提供：

```bash
docker compose up --build
```

发行环境未必包含 Docker，因此只有实际执行后才能把容器结果计入验收。

## 8. 开源治理

- 软件：Apache License 2.0；
- 合成示例数据和项目文档：除另行说明外，建议按 CC BY 4.0 复用并保留来源与边界；
- 贡献：见 `CONTRIBUTING.md`；
- 治理：见 `GOVERNANCE.md`；
- 安全报告：见 `SECURITY.md`；
- 临床与数据边界：见 `DATA_AND_CLINICAL_BOUNDARY.md`；
- 90 天落地：见 `docs/12_90_day_pilot.md`。

## 9. 项目结构

```text
pamchina/       主动医学工作流、接口、MPI、审计与展示服务
dikwp_mesh81/   DIKWP MESH8.1 双向语义连续性运行时
web/            响应式浏览器工作台与单文件离线展示
data/           24 服务包、9 条合成人群旅程、知识与网络目录
schemas/        JSON Schema
config/         连接器、字段映射、身份角色和生产检查样例
docs/           架构、实施、治理、接口、SIT/UAT 与试点手册
tests/          自动化测试
tools/          QA、静态审计、验收和发行清单工具
```

## 10. 项目来源与独立性

本项目继承并扩展段玉聪公开 GitHub 生态中的 DIKWP、主动医学及浦东中医工作流工程成果，形成全国可复制的主动医学开源参考实现。它不表示任何医院、政府部门、标准组织、期刊或参考主体委托、背书、采购、验收或上线。
