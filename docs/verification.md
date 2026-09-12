# 发布核验记录 / Publication verification

核验日期 / Inspection date: **2026-09-12**

## 文件完整性 / File integrity

- 用户提供的模型目录共 217 个文件，合计 221,436,406 字节。发布副本逐文件 SHA-256 与源文件及首次清单一致。
- 217 supplied CAD files total 221,436,406 bytes. SHA-256 checks of the publication copy match the source files and the initial manifest for every file.
- 全部模型原文件名和内部目录保留；未重新保存原生 CAD 或重新生成 STEP。答辩 PPT 不在仓库内。
- All original model filenames and internal directories are preserved. Native CAD was not resaved and STEP files were not regenerated. The presentation is excluded.
- [model-inventory.csv](model-inventory.csv) 记录路径、类型、大小及哈希；[SHA256SUMS.txt](SHA256SUMS.txt) 为完整模型校验清单。
- The inventory records path, type, size and hash. The checksum file covers every supplied CAD file.

## CAD 查看 / CAD inspection

| 检查 / Check | 结果 / Result |
| --- | --- |
| 软件 / Application | SOLIDWORKS 2025 SP3.0，API revision 33.3.0 |
| 查看方式 / Viewing | 发布副本设为只读，OpenDoc6 使用 Silent + ReadOnly；激活视图时明确不重建 / Read-only copy; Silent + ReadOnly opening; activation without rebuild |
| 原生模型直接查看并导图 / Native models viewed and illustrated | 总装、收割、播种、翻土、车架、张紧子装配 / Overall assembly, harvesting, planting, soil working, chassis and tensioner |
| 总装组件 / Main-assembly instances | 346；GetSuppression 均为 2（完全解析）/ All returned state 2 (fully resolved) |
| 虚拟零件 / Virtual part | 1 个内嵌零件，2 个实例 / One embedded part, two instances |
| 总装依赖 / Main-assembly dependencies | 67 项：66 个包内外部文件 + 1 个内嵌虚拟零件 / 66 in-package external files plus one embedded virtual part |
| 全部装配与图纸的引用检查 / All assembly/drawing dependencies | 18 个装配体 + 3 张图纸均读取依赖 / Dependencies read for all 18 assemblies and 3 drawings |
| 历史引用缺口 / Historical gaps | 2 张工程图、8 个镜向铰链装配；合计 4 个不同的缺失文件名 / Two drawings and eight mirrored-hinge assemblies; four distinct missing filenames |
| 模型内容 / CAD content | 源文件与发布副本全部哈希一致 / All source and publication hashes match |

主要模型再次只读打开时，API 返回加载错误 0、警告 130。130 是 `ReadOnly (2)` 与 `AlreadyOpen (128)` 的组合，不代表模型树中的特征/配合已无警告。SOLIDWORKS 模型树中确实可见既有特征/配合警告，未作修改。

Reopening the main inspected models read-only returned load error 0 and warning 130. This combines `ReadOnly (2)` and `AlreadyOpen (128)`; it does not establish a warning-free feature/mate tree. Existing feature/mate warnings were visible and were not repaired.

详细清单：[总装组件实例 / Main assembly instances](assembly-components.csv)、[装配与工程图依赖 / Assembly and drawing dependencies](dependency-audit.json)。组件清单是当前配置的实例导出，不是已经完成采购、加工或成本核算的 BOM。

The component list is an instance export for the inspected configuration, not a procurement, manufacturing or costed BOM.

## 本次未验证 / Not verified in this release

未对 217 个文件逐一完成图形与几何质量验收，也未进行全配置遍历、强制重建、配合修复、干涉检测、运动/动力学仿真、有限元分析、完整材料与公差审核、制造工艺验证或田间试验。当前加载成功不能替代这些工程验证。未对 STEP 与原生模型做逐实体一致性比对；另外两张历史工程图不能凭引用清单声称已能完整重建。

This release does not individually certify the geometry of all 217 files, traverse every configuration, force a rebuild, repair mates, check interference, perform motion/dynamic simulation or FEA, audit all materials and tolerances, validate manufacturing processes or conduct field tests. Successful loading is not a substitute for those checks. STEP/native entity equivalence was not tested, and the two historical drawings are not certified to rebuild completely.

## API 判据来源 / API reference

- [Component resolution states](https://help.solidworks.com/2023/English/api/swconst/SolidWorks.Interop.swconst~SolidWorks.Interop.swconst.swComponentSuppressionState_e.html)
- [File load warning bitmask](https://help.solidworks.com/2026/english/api/swconst/SolidWorks.Interop.swconst~SolidWorks.Interop.swconst.swFileLoadWarning_e.html)
- [Document dependencies](https://help.solidworks.com/2019/english/api/sldworksapi/SOLIDWORKS.Interop.sldworks~SOLIDWORKS.Interop.sldworks.ISldWorks~GetDocumentDependencies2.html)
- [View bitmap export](https://help.solidworks.com/2021/English/api/sldworksapi/SolidWorks.Interop.sldworks~SolidWorks.Interop.sldworks.IModelDoc2~SaveBMP.html)
