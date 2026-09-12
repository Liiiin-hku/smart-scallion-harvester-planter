# 模型查看指南 / Model viewing guide

[项目首页 / Project](../README.md) · [机构详解 / Walkthrough](mechanical-design.md)

## 推荐查看顺序 / Suggested sequence

| 顺序 / Order | 文件 / File | 用途 / Purpose |
| --- | --- | --- |
| 1 | `cad/大葱收种一体机/大葱收割机.SLDASM` | 总装与空间布局 / Main assembly and layout |
| 2 | 同目录 / Same directory: `收割部分.SLDASM` | 扶葱、松土、输送及张紧 / Guiding, loosening, conveying and tensioning |
| 3 | `播种部分.SLDASM`、`翻土.SLDASM` | 播种与土壤作业 / Planting and soil working |
| 4 | `车架.SLDPRT`、`输送带导向轮2张紧.SLDASM` | 支承及局部结构 / Frame and mechanism detail |
| 5 | `大葱收割机.SLDDRW` | 已有整机工程图 / Existing overall drawing |

## 下载与引用 / Download and references

完整下载仓库并解压后再打开。不要只下载一个 `.SLDASM`，也不要把标准件与子装配从原目录中移走。模型包内部目录和文件名保持原样，只有外层增加 `cad/` 归档目录。

Download and extract the complete repository. A single `.SLDASM` file is insufficient. Keep hardware and subassembly files in their original folders. Internal filenames and folder relationships are preserved; only the outer `cad/` directory has been added for repository organization.

若 SOLIDWORKS 询问引用位置，先指向 `cad/大葱收种一体机/`，再根据文件名定位 `标件/`、`轮子/` 或原气缸子目录。可以只读查看，避免软件版本转换或重建操作写回文件。原生文件的保存版本未逐个确认；本次实测查看环境为 SOLIDWORKS 2025 SP3.0。已有总装 STEP 头部标识为 SolidWorks 2022 / AP214，但这不证明所有原生文件都能用 2022 打开。

If SOLIDWORKS asks for a reference location, point it to the model directory and then the appropriate hardware, wheel or cylinder subfolder. Read-only viewing avoids writing version conversions or rebuild changes back to the files. Native save versions have not been verified individually. The viewing environment used for this release was SOLIDWORKS 2025 SP3.0. The existing main STEP header identifies SolidWorks 2022 / AP214; this does not prove that every native file can be opened in 2022.

## STEP 与工程图 / STEP files and drawings

`大葱收割机.STEP` 是已有整机交换模型，适合支持 STEP 的 CAD 查看工具。STEP 不保留与原生 SOLIDWORKS 相同的参数化历史和配合编辑体验。保留的 110 个 STEP 中包含不同目录下的同名文件，未擅自去重；它们是原始交付的一部分。三张原有工程图全部保留，但其中两张有下列历史引用缺口。

The existing `大葱收割机.STEP` is a neutral-format overall model for compatible CAD viewers. It does not offer the same parametric history and mate-editing workflow as native SOLIDWORKS. All 110 existing STEP files are retained, including same-named files in different folders; none were deduplicated. All three original drawings are included, with the historical reference gaps below.

<a id="known-reference-gaps"></a>
## 已知引用缺口 / Known reference gaps

| 受影响文件 / Affected files | 当前文件夹未提供的引用 / Referenced files not supplied |
| --- | --- |
| `履带原版.SLDDRW` | `履带原版.SLDASM` |
| `拆解.SLDDRW` | `拆解.SLDASM` |
| `标件/镜向活动铰链[CT-20-2020].step.SLDASM` 及 / and `.step1.SLDASM` 至 / through `.step7.SLDASM`，共 8 个 / 8 files | `镜向_CT1-20-2020.step.SLDPRT`、`镜向_CT2-20-2020.step.SLDPRT` |

这些文件按原样保留，不应把其独立重建完整性视为已验证。当前总装加载的是可解析的非镜向铰链链路，上述缺口未出现在总装的实际引用链中。不要将缺失的镜向件直接替换为非镜向件；几何与装配关系可能不同。`履带原版.SLDDRW` 的历史文件名也不代表当前四轮总装采用履带结构。

These files are retained unchanged, and their standalone rebuild completeness is not verified. The active main assembly resolves the non-mirrored hinge chain; these gaps are outside its inspected dependency chain. Do not substitute non-mirrored parts for missing mirrored parts without design review. The historical tracked-version drawing filename does not describe the four-wheel layout of the current main assembly.

`零件5^收割部分.SLDPRT` 为 `收割部分.SLDASM` 内嵌的虚拟零件，在总装中有两个实例。SOLIDWORKS 会把它临时展开到运行时缓存，它不是需要另外上传的外部零件。引用清单以 `embedded_virtual: true` 标记该项。

`零件5^收割部分.SLDPRT` is a virtual part embedded in `收割部分.SLDASM`, with two instances in the main assembly. SOLIDWORKS temporarily expands it into a runtime cache; no separate external file needs uploading. The audit marks it as `embedded_virtual: true`.

## 保留原模型状态 / Preserved model state

查看时，模型树中可见部分特征/配合警告。本次仅检查加载、引用与可见结构，没有执行全模型重建、配合修复、干涉检查、运动仿真、有限元分析或制造验收。需要工程修改时，请在副本或独立分支进行，并记录变化；本次发布的模型与用户提供文件逐字节一致。

Some feature/mate warnings were visible in the model tree. This release checks loading, references and visible structure; it does not certify a full rebuild, mate repair, interference check, motion simulation, finite-element analysis or manufacturing readiness. Make engineering changes in a separate copy or branch and record them. Published CAD files are byte-for-byte identical to the supplied files.
