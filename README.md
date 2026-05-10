<p align="center">
  <img src="assets/banner.png" alt="Hermes Agent" width="100%">
</p>

Hermes Agent ☤

<p align="center">
  <a href="https://hermes-agent.nousresearch.com/docs/"><img src="https://img.shields.io/badge/Docs-hermes--agent.nousresearch.com-FFD700?style=for-the-badge" alt="文件"><\/a>
  <a href="https://discord.gg/NousResearch"><img src="https://img.shields.io/badge/Discord-5865F2?style=for-the-badge&logo=discord&logoColor=white" alt="Discord"><\/a>
  <a href="https://github.com/NousResearch/hermes-agent/blob/main/LICENSE"><img src="https://img.shields.io/badge/License-MIT-green?style=for-the-badge" alt="授權條款: MIT"><\/a>
  <a href="https://nousresearch.com"><img src="https://img.shields.io/badge/Built%20by-Nous%20Research-blueviolet?style=for-the-badge" alt="由 Nous Research 開發"><\/a>
  <a href="README.zh-CN.md"><img src="https://img.shields.io/badge/Lang-中文-red?style=for-the-badge" alt="中文"><\/a>
</p>

由 Nous Research 開發的自我改進 AI 代理。 它是唯一具有內建學習迴圈的代理 —— 能從經驗中創建技能、在使用過程中自我提升、推動自己持久記憶、搜尋過往對話，並建立跨會話的個人深度模型。可在 5 美元的 VPS、GPU 叢集、或幾乎零閒置成本的無伺服器架構上運行。它不依賴你的筆電 —— 你可以在 Telegram 與它對話，同時它在雲端 VM 工作。

可使用任何模型 —— Nous Portal、OpenRouter（200+ 模型）、NVIDIA NIM（Nemotron）、Xiaomi MiMo、z.ai/GLM、Kimi/Moonshot、MiniMax、Hugging Face、OpenAI，或自建端點。使用 hermes model 即可切換 —— 無需改碼、無綁定。

<table>
<tr><td>真實終端介面</td><td>完整 TUI，支援多行編輯、斜線命令自動補全、對話歷史、可中斷與重導向、串流工具輸出。</td></tr>
<tr><td>隨處可用</td><td>Telegram、Discord、Slack、WhatsApp、Signal、CLI —— 皆可透過單一網關程序運行。支援語音備忘錄轉錄、跨平台連續對話。</td></tr>
<tr><td>封閉學習迴圈</td><td>代理策劃的記憶並定期提示。複雜任務後自動生成技能。技能在使用中自我提升。FTS5 會話搜尋結合 LLM 摘要以跨會話回顧。<a href="https://github.com/plastic-labs/honcho">Honcho</a> 辯證用戶建模。兼容 <a href="https://agentskills.io">agentskills.io</a> 開放標準。</td></tr>
<tr><td>排程自動化</td><td>內建 cron 排程器，可送達任何平台。每日報告、夜間備份、每週稽核 —— 自然語言運行，無需看守。</td></tr>
<tr><td>分派並平行處理</td><td>可生成隔離子代理以並行工作流。撰寫 Python 腳本透過 RPC 調用工具，將多步流程壓縮為零上下文成本的互動。</td></tr>
<tr><td>能運行於任何地方</td><td>七種終端後端 —— 本地、Docker、SSH、Singularity、Modal、Daytona、Vercel Sandbox。Daytona 和 Modal 提供無伺服器持久化 —— 代理環境閒置時休眠、按需喚醒，會話間幾乎零成本。可運行於 $5 VPS 或 GPU 叢集。</td></tr>
<tr><td>研究就緒</td><td>批量軌跡生成、Atropos 強化學習環境、軌跡壓縮以訓練下一代工具調用模型。</td></tr>
</table>

---

快速安裝

Linux、macOS、WSL2、Termux

curl -fsSL https://raw.githubusercontent.com/NousResearch/hermes-agent/main/scripts/install.sh | bash

Windows（原生、PowerShell）—— 早期測試版

> 注意： 原生 Windows 支援為 早期測試版。可安裝與運行，但尚未像 Linux/macOS/WSL2 路徑那樣廣泛測試。如遇問題請提交 Issue。若想要最穩定的 Windows 設定，建議在 WSL2 內執行上方 Linux/macOS 一鍵安裝。

於 PowerShell 執行：

irm https://raw.githubusercontent.com/NousResearch/hermes-agent/main/scripts/install.ps1 | iex

安裝程式會自動處理：uv、Python 3.11、Node.js、ripgrep、ffmpeg，以及可攜式 Git Bash（MinGit，解壓至 %LOCALAPPDATA%\\hermes\\git —— 無需管理員權限，完全獨立於系統 Git 安裝）。Hermes 使用此內建 Git Bash 執行 shell 指令。

若系統已有 Git，安裝程式會自動偵測並使用。否則會下載約 45MB 的 MinGit —— 不會影響系統 Git。

> Android / Termux： 已測試的手動流程記錄在 Termux 指南。Hermes 在 Termux 會安裝精選的 .[termux] 依賴，因完整的 .[all] 目前包含 Android 不支援的語音套件。
>
> Windows： 原生 Windows 支援為 早期測試版 —— 上述 PowerShell 一鍵安裝即可，但可能有小問題，請回報。若傾向使用 WSL2（最穩定路徑），可執行 Linux 指令。原生 Windows 安裝位於 %LOCALAPPDATA%\\hermes；WSL2 則如 Linux 於 ~/.hermes。當前唯一需要 WSL2 的功能是瀏覽器儀表板對話窗（使用 POSIX PTY —— 傳統 CLI 與網關可原生運行）。

安裝後：

source ~/.bashrc    # 重新載入 shell（或：source ~/.zshrc）
hermes              # 開始聊天！

---

入門教學

hermes              # 互動式 CLI —— 開始對話
hermes model        # 選擇 LLM 提供者與模型
hermes tools        # 設定啟用哪些工具
hermes config set   # 設置單一設定值
hermes gateway      # 啟動訊息網關（Telegram、Discord 等）
hermes setup        # 執行完整設定精靈（一次完成所有設定）
hermes claw migrate # 從 OpenClaw 遷移
hermes update       # 更新至最新版本
hermes doctor       # 診斷任何問題

📖 完整文件 →

CLI 與訊息平台快速對照

Hermes 有兩種入口：終端 TUI hermes，或啟動網關後從 Telegram、Discord、Slack、WhatsApp、Signal、Email 對話。一旦進入對話，多數斜線命令可通用。

動作
CLI
訊息平台
開始聊天
hermes
執行 hermes gateway setup + hermes gateway start，然後傳訊給機器人
開新對話
/new 或 /reset
/new 或 /reset
更換模型
/model [provider:model]
/model [provider:model]
設定人格
/personality [name]
/personality [name]
重試或撤銷上一輪
/retry、/undo
/retry、/undo
壓縮上下文 / 查看用量
/compress、/usage、/insights [--days N]
/compress、/usage、/insights [days]
瀏覽技能
/skills 或 /<skill-name>
/<skill-name>
中斷當前工作
Ctrl+C 或傳新訊息
/stop 或傳新訊息
平台狀態
/platforms
/status、/sethome

完整指令列表請見 CLI 指南 與 訊息網關指南。

---

文件

所有文件位於 hermes-agent.nousresearch.com/docs：

區塊
內容
快速開始
安裝 → 設定 → 2 分鐘內開始對話
CLI 使用
指令、快捷鍵、人格、會話
設定
設定檔、提供者、模型、所有選項
訊息網關
Telegram、Discord、Slack、WhatsApp、Signal、Home Assistant
安全性
指令審核、私訊配對、容器隔離
工具與工具集
40+ 工具、工具集系統、終端後端
技能系統
程序化記憶、技能中心、建立技能
記憶
持久記憶、用戶檔案、最佳實踐
MCP 整合
連接任何 MCP 伺服器以擴展能力
Cron 排程
平台配送的排程任務
上下文檔案
影響每次對話的專案上下文
架構
專案結構、代理迴圈、核心類別
貢獻指南
開發環境、PR 流程、程式風格
CLI 參考
所有指令與旗標
環境變數
完整環境變數參考

---

從 OpenClaw 遷移

若你來自 OpenClaw，Hermes 可自動導入設定、記憶、技能、API 金鑰。

首次設定時： 設定精靈 (hermes setup) 會自動偵測 ~/.openclaw 並在設定前提供遷移選項。

安裝後任何時刻：

hermes claw migrate              # 互動式遷移（完整預設）
hermes claw migrate --dry-run    # 預覽將遷移內容
hermes claw migrate --preset user-data   # 遷移但不含機密
hermes claw migrate --overwrite  # 覆蓋現有衝突

導入項目：
SOUL.md — 人格檔案
Memories — MEMORY.md 與 USER.md
Skills — 用戶技能 → ~/.hermes/skills/openclaw-imports/
指令允許清單 — 審核模式
訊息設定 — 平台、允許用戶、工作目錄
API 金鑰 — 允許的機密（Telegram、OpenRouter、OpenAI、Anthropic、ElevenLabs）
TTS 資源 — 工作區音訊檔
工作區指令 — AGENTS.md（使用 --workspace-target）

詳見 hermes claw migrate --help，或使用 openclaw-migration 技能進行互動式代理遷移與預覽。

---

貢獻

歡迎貢獻！請見 貢獻指南 了解開發設定、程式風格與 PR 流程。

貢獻者快速開始 —— clone 後直接執行 setup-hermes.sh：

git clone https://github.com/NousResearch/hermes-agent.git
cd hermes-agent
./setup-hermes.sh     # 安裝 uv、建立 venv、安裝 .[all]、symlink hermes 到 ~/.local/bin
./hermes              # 自動偵測 venv，無需先 source

手動路徑（等效於上述）：

curl -LsSf https://astral.sh/uv/install.sh | sh
uv venv .venv --python 3.11
source .venv/bin/activate
uv pip install -e ".[all,dev]"
scripts/run_tests.sh

> RL 訓練（選用）： RL/Atropos 整合（environments/）—— 參見 CONTRIBUTING.md 完整設定流程。

---

社群

💬 Discord
📚 Skills Hub
🐛 問題回報
🔌 HermesClaw —— 社群 WeChat 橋接：同時運行 Hermes Agent 與 OpenClaw 於同一個 WeChat 帳號。

---

授權

MIT —— 見 LICENSE。

由 Nous Research 開發。