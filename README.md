# 完整脱敏源码下载

本项目以 MIT 许可证公开完整源码。**请先下载并解压 [hotel-tv-agent-sanitized-source.zip](./hotel-tv-agent-sanitized-source.zip)，再按下方说明运行。**

源码包包含全部 53 个经审查的源码、构建配置、演示素材和许可证文件，不含原 Git 历史、实际密钥、数据库、聊天、录音、签名材料或原私有媒体。模型和运行库按包内脚本另行下载。

网页浏览目录目前正在分批整理，仓库根目录的源码包是完整可用的公开分发版本。请勿直接在尚未整理齐全的网页目录上执行构建。

```powershell
Expand-Archive ./hotel-tv-agent-sanitized-source.zip ./source
cd source
```

源码包 SHA-256：`d073a0303bb3d9e3be7b28ad4efa209256577458e61f25248bdf8640cf656a9b`。验证边界见解压后的 `docs/VALIDATION.md`；自动化验证不代表真实模型或真机验收。

---

# Hotel TV Agent · 酒店电视智能体原型

MIT 开源的本地酒店TV/网页/安卓演示：React + FastAPI + SQLite。提供陪伴管家、演示设备状态、知识库问答、天气/公开检索与退房清理流程；安卓源码基于原目录的 3.5 客户端。

**酒店、设备、频道与知识库为演示；没有接入真实酒店/PMS/客房控制器或真实电视直播。** 原业务数据库、知识库内容、文档、照片、日志、安装包与 Git 历史未分发。媒体使用新生成的 MIT 占位素材。

## 本地启动

需要 Python 3.11、Node.js 20+。仓库根目录：

```powershell
python -m venv backend/.venv
backend/.venv/Scripts/python -m pip install -r backend/requirements.txt
Copy-Item .env.example .env
cd frontend
npm ci
npm run build
cd ..
backend/.venv/Scripts/python backend/main.py
```

访问 `http://127.0.0.1:8000`。没有密钥时运行明确的本地兜底回复，灯光/空调/窗帘只更新本地演示状态。需要模型时在自己的 `.env` 设置 API 地址、模型名和密钥；调用模型/在线语音可能产生服务费用。运行数据在 `data/`，不要提交。

默认监听 loopback。只有你明确配置 `HOTEL_HOST=0.0.0.0` 才提供局域网服务；本原型没有生产用户鉴权和客房隔离，不应直接暴露公网。

## 安卓源码

准备 JDK 17 和 Android SDK 35（可通过Android Studio安装），在仓库根目录：

```powershell
python scripts/fetch_android_model.py
python scripts/android_gradle.py assembleDebug
```

安卓首次在设置中填自己的 API 地址、模型和密钥；无内置运营方密钥。输入隐藏显示，保存使用 Android Keystore 加密，旧本地明文偏好迁移后删除。未分发签名材料或 APK。手机助手权限需使用者在系统中明确授予；设备动作是原型，不宣称能控制实际酒店设施。

Vosk 中文小模型由脚本从官方站点下载，不放在仓库；上游模型标注 Apache-2.0。Gradle工具单独下载校验，Android依赖由公开仓库取得。

## 开源边界

只发布经过筛选的源码与演示配置，采用全新 Git 历史。酒店知识库种子换成无真实地址、联系方式、WiFi密码或服务承诺的示例信息。原客户资料与运行数据不读取、不复用。构建脚本不往源码或APK注入模型密钥。

本次构建与API测试用隔离数据、无真实模型密钥；不是生产酒店部署验收。项目代码 MIT，依赖许可分别保留，详见 `NOTICE.md`、`SECURITY.md` 和 `docs/ASSETS.md`。

