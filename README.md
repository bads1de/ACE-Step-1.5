<h1 align="center">ACE-Step 1.5</h1>
<h1 align="center">オープンソース音楽生成の限界を押し広げる</h1>
<p align="center">
    <a href="https://ace-step.github.io/ace-step-v1.5.github.io/">プロジェクト</a> |
    <a href="https://huggingface.co/ACE-Step/Ace-Step1.5">Hugging Face</a> |
    <a href="https://modelscope.cn/models/ACE-Step/Ace-Step1.5">ModelScope</a> |
    <a href="https://huggingface.co/spaces/ACE-Step/Ace-Step-v1.5">デモ (Space)</a> |
    <a href="https://discord.gg/PeWDxrkdj7">Discord</a> |
    <a href="https://arxiv.org/abs/2602.00744">テクニカルレポート</a>
</p>

<p align="center">
    <img src="./assets/orgnization_logos.png" width="100%" alt="StepFun Logo">
</p>

## 目次

- [✨ 特徴](#-特徴)
- [📦 インストール](#-インストール)
- [📥 モデルのダウンロード](#-モデルのダウンロード)
- [🚀 使い方](#-使い方)
- [📖 チュートリアル](#-チュートリアル)
- [🔨 学習](#-学習)
- [🏗️ アーキテクチャ](#️-アーキテクチャ)
- [🦁 モデル Zoo](#-モデル-zoo)

## 📝 概要

🚀 私たちは、商用グレードの生成品質をコンシューマー向けハードウェアで実現する、高効率なオープンソース音楽基盤モデル **ACE-Step v1.5** を紹介します。一般的な評価指標において、ACE-Step v1.5は多くの商用音楽モデルを超える品質を達成しながら、A100でフルソング生成に2秒未満、RTX 3090で10秒未満という極めて高速な動作を実現しています。このモデルは4GB未満のVRAMでローカル動作し、軽量なパーソナライズ（LoRA）にも対応しており、ユーザーは数曲のデータから独自のスタイルを学習させることが可能です。

🌉 その核心には、Language Model (LM) が万能なプランナーとして機能する新しいハイブリッドアーキテクチャがあります。LMは単純なユーザークエリを包括的な楽曲の設計図（短いループから10分の楽曲まで）に変換し、Chain-of-Thought（思考の連鎖）を通じてメタデータ、歌詞、キャプションを合成し、Diffusion Transformer (DiT) をガイドします。⚡ 独自の特徴として、この整合性はモデルの内部メカニズムのみに依存した内発的強化学習によって達成されており、外部の報酬モデルや人間の好みに起因するバイアスを排除しています。🎚️

🔮 標準的な合成を超えて、ACE-Step v1.5は、カバー生成、リペイント（部分修正）、ボーカルからBGMへの変換など、多彩な編集機能と正確なスタイル制御を統合し、50以上の言語でのプロンプト遵守を維持しています。これは、音楽アーティスト、プロデューサー、コンテンツクリエイターのワークフローにシームレスに統合される強力なツールへの道を切り開きます。🎸

## ✨ 特徴

<p align="center">
    <img src="./assets/application_map.png" width="100%" alt="ACE-Step Framework">
</p>

### ⚡ パフォーマンス

- ✅ **超高速生成** — A100でフルソング生成2秒未満、RTX 3090で10秒未満（思考モードと拡散ステップにより0.5秒〜10秒）
- ✅ **柔軟な長さ** — 10秒から10分（600秒）の音声生成をサポート
- ✅ **バッチ生成** — 最大8曲を同時に生成可能

### 🎵 生成品質

- ✅ **商用グレードの出力** — 多くの商用音楽モデルを超える品質（Suno v4.5とSuno v5の間）
- ✅ **豊富なスタイルサポート** — 1000以上の楽器とスタイル、詳細な音色記述に対応
- ✅ **多言語歌詞** — 50以上の言語に対応し、歌詞プロンプトによる構造とスタイルの制御が可能

### 🎛️ 汎用性と制御

| 機能                  | 説明                                                               |
| --------------------- | ------------------------------------------------------------------ |
| ✅ 参照オーディオ入力 | 参照オーディオを使用して生成スタイルをガイド                       |
| ✅ カバー生成         | 既存のオーディオからカバーを作成                                   |
| ✅ リペイント & 編集  | 特定部分のオーディオ編集と再生成                                   |
| ✅ トラック分離       | オーディオを個々のステム（パート）に分離                           |
| ✅ マルチトラック生成 | Suno Studioの「レイヤー追加」のような機能                          |
| ✅ Vocal2BGM          | ボーカルトラックの伴奏を自動生成                                   |
| ✅ メタデータ制御     | 長さ、BPM、キー/スケール、拍子の制御                               |
| ✅ シンプルモード     | 簡単な説明からフルソングを生成                                     |
| ✅ クエリ書き換え     | LMによるタグと歌詞の自動拡張                                       |
| ✅ オーディオ理解     | オーディオからBPM、キー/スケール、拍子、キャプションを抽出         |
| ✅ LRC生成            | 生成された音楽の歌詞タイムスタンプを自動生成                       |
| ✅ LoRA学習           | Gradioでのワンクリック注釈＆学習。RTX 3090 (12GB VRAM) で8曲/1時間 |
| ✅ 品質スコアリング   | 生成されたオーディオの自動品質評価                                 |

## 最新情報を入手

---

GitHubでACE-Stepにスターをつけて、新着リリースを即座に通知してもらいましょう
![](assets/star.gif)

## 📦 インストール

> **必須要件:** Python 3.11, CUDA GPU 推奨 (CPU/MPSでも動作しますが遅くなります)

### CPU サポート (限定的)

ACE-StepはCPUで**推論のみ**実行可能ですが、パフォーマンスは著しく低下します。

- CPU推論はテストや実験用にサポートされています。
- **CPUでの学習 (LoRAを含む) は推奨されません**。実行時間が極端に長くなるためです。
- 低VRAMシステムの場合、DiTのみのモード (LLM無効) がサポートされています。
- CPU学習は技術的には実行可能かもしれませんが、実用的ではありません。**実用的な学習ワークフローには、CUDA対応GPUまたはクラウドGPUインスタンスが必要です。**

CUDA GPUをお持ちでない場合は、以下をご検討ください：

- クラウドGPUプロバイダーの利用
- 推論のみのワークフローの実行
- `ACESTEP_INIT_LLM=false` を設定したDiTのみのモードの使用

### AMD / ROCm GPU

ACE-StepはPyTorch ROCmビルドを通じてAMD GPUで動作します。

**重要:** `uv run acestep` ワークフローは現在CUDA PyTorchホイールをインストールするため、既存のROCm設定を上書きする可能性があります。`uv run acestep` はCUDA環境に最適化されており、ROCm PyTorchインストールを無効にする可能性があります。

#### AMD / ROCm ユーザー向け推奨ワークフロー

1. 仮想環境を手動で作成し、有効化します：

   ```bash
   python -m venv .venv
   source .venv/bin/activate
   ```

2. ROCm互換のPyTorchビルドをインストールします：

   ```bash
   pip install torch --index-url https://download.pytorch.org/whl/rocm6.0
   ```

3. `uv run` を使用せずにACE-Stepの依存関係をインストールします：

   ```bash
   pip install -e .
   ```

4. サービスを直接起動します：

   ```bash
   python -m acestep.acestep_v15_pipeline --port 7680
   ```

これにより、CUDAホイールによる置き換えを防ぎ、ROCmシステムでの動作確認がされています。Windowsの場合は、`.venv\Scripts\activate` を使用して同様の手順を行ってください。

#### GPU検出のトラブルシューティング

AMD GPUを使用しているのに "No GPU detected, running on CPU" と表示される場合：

1. GPU診断ツールを実行します：

   ```bash
   python scripts/check_gpu.py
   ```

2. RDNA3 GPU (RX 7000/9000 シリーズ) の場合、`HSA_OVERRIDE_GFX_VERSION` を設定します：
   - RX 7900 XT/XTX, RX 9070 XT: `export HSA_OVERRIDE_GFX_VERSION=11.0.0` (Linux) または `set HSA_OVERRIDE_GFX_VERSION=11.0.0` (Windows)
   - RX 7800 XT, RX 7700 XT: `export HSA_OVERRIDE_GFX_VERSION=11.0.1`
   - RX 7600: `export HSA_OVERRIDE_GFX_VERSION=11.0.2`

3. Windowsでは、必要な環境変数を自動的に設定する `start_gradio_ui_rocm.bat` を使用してください。

4. ROCmインストールの確認: `rocm-smi` でGPUが表示されるか確認してください。

### AMD / ROCM Linux 固有 (cachy-os テスト済み)

このプログラムが動作確認された日付:
2026年2月7日 - 10:40 am UTC +1

cachy-os用およびRDNA4でテスト済みのACE-Step1.5 Rocmマニュアル。
`docs\en\ACE-Step1.5-Rocm-Manual-Linux.md` を参照してください。

### Linux + Python 3.11 に関する注意

一部のLinuxディストリビューション (Ubuntuを含む) には、Python 3.11.0rc1 という **プレリリース** ビルドが含まれている場合があります。このバージョンは、C拡張の非互換性により、vLLMバックエンドの使用時にセグメンテーション違反を引き起こすことが知られています。

**推奨:** 安定版のPythonリリース (≥ 3.11.12) を使用してください。Ubuntuでは、deadsnakes PPAを介してインストールできます。

Pythonのアップグレードが不可能な場合は、PyTorchバックエンドを使用してください：

```bash
uv run acestep --backend pt
```

### 🪟 Windows ポータブルパッケージ (Windows 推奨)

Windowsユーザー向けに、依存関係がインストール済みのポータブルパッケージを提供しています：

1. ダウンロードして解凍: [ACE-Step-1.5.7z](https://files.acemusic.ai/acemusic/win/ACE-Step-1.5.7z)
2. パッケージにはすべての依存関係が含まれた `python_embeded` が同梱されています
3. **要件:** CUDA 12.8

#### 🚀 クイックスタートスクリプト

ポータブルパッケージには、簡単に操作できる便利なバッチスクリプトが含まれています：

| スクリプト               | 説明                    | 使用法                                 |
| ------------------------ | ----------------------- | -------------------------------------- |
| **start_gradio_ui.bat**  | Gradio Web UI を起動    | ダブルクリックまたはターミナルから実行 |
| **start_api_server.bat** | REST API サーバーを起動 | ダブルクリックまたはターミナルから実行 |

**基本的な使用法:**

```bash
# Gradio Web UI を起動 (推奨)
start_gradio_ui.bat

# REST API サーバーを起動
start_api_server.bat
```

両方のスクリプトは以下をサポートしています：

- ✅ 自動環境検出 (`python_embeded` または `uv`)
- ✅ 必要に応じて `uv` を自動インストール (winget または PowerShell 経由)
- ✅ 設定可能なダウンロードソース (HuggingFace/ModelScope)
- ✅ 起動前のオプションの Git アップデートチェック
- ✅ カスタマイズ可能なモデルとパラメータ

#### 📝 設定

スクリプトを編集して設定をカスタマイズできます：

**start_gradio_ui.bat:**

```batch
REM UI 言語 (en, zh, he, ja)
set LANGUAGE=ja

REM ダウンロードソース (auto, huggingface, modelscope)
set DOWNLOAD_SOURCE=--download-source modelscope

REM Git アップデートチェック (true/false) - PortableGitが必要
set CHECK_UPDATE=true

REM モデル設定
set CONFIG_PATH=--config_path acestep-v15-turbo
set LM_MODEL_PATH=--lm_model_path acestep-5Hz-lm-1.7B

REM LLM 初期化 (auto/true/false)
REM Auto: VRAM > 6GBなら有効、それ以外は無効
REM set INIT_LLM=--init_llm true   # 強制有効化 (低VRAMではOOMの原因になる可能性あり)
REM set INIT_LLM=--init_llm false  # 強制無効化 (DiTのみモード)
```

**start_api_server.bat:**

```batch
REM 環境変数によるLLM初期化
REM set ACESTEP_INIT_LLM=true   # LLMを強制有効化
REM set ACESTEP_INIT_LLM=false  # LLMを強制無効化 (DiTのみモード)

REM LM モデルパス (オプション)
REM set LM_MODEL_PATH=--lm-model-path acestep-5Hz-lm-0.6B
```

#### 🔄 アップデート & メンテナンスツール

| スクリプト              | 目的                                    | 使用タイミング                                |
| ----------------------- | --------------------------------------- | --------------------------------------------- |
| **check_update.bat**    | GitHubからチェックしてアップデート      | 最新バージョンに更新したい時                  |
| **merge_config.bat**    | バックアップされた設定を統合            | アップデート後に設定の競合が発生した時        |
| **install_uv.bat**      | uv パッケージマネージャーをインストール | 起動中にuvのインストールに失敗した場合        |
| **quick_test.bat**      | 環境設定をテスト                        | 環境が動作しているか確認するため              |
| **test_git_update.bat** | Git アップデート機能をテスト            | PortableGitが正しく動作しているか確認するため |

**アップデートワークフロー:**

```bash
# 1. アップデートを確認 (PortableGit/ が必要)
check_update.bat

# 2. 競合が発生した場合、変更は自動的にバックアップされます
# 3. アップデート後、設定をマージして戻します
merge_config.bat

# オプション:
# - バックアップと現在のファイルを比較 (メモ帳で並べて表示)
# - バックアップからファイルを復元
# - バックアップされたすべてのファイルを一覧表示
# - 古いバックアップを削除
```

**環境テスト:**

```bash
# セットアップをテスト
quick_test.bat

# これにより以下がチェックされます:
# - Python インストール (python_embeded または システム Python)
# - uv インストールと PATH
# - GPU 可用性 (CUDA/ROCm)
# - 基本的なインポート
```

#### 📦 Portable Git サポート

パッケージに `PortableGit/` フォルダがある場合、以下が可能です：

1. **自動アップデートの有効化:** `start_gradio_ui.bat` または `start_api_server.bat` を編集

   ```batch
   set CHECK_UPDATE=true
   ```

2. **手動アップデートチェック:**

   ```bash
   check_update.bat
   ```

3. **競合処理:** 修正したファイルがGitHubの更新と競合する場合：
   - ファイルは自動的に `.update_backup_YYYYMMDD_HHMMSS/` にバックアップされます
   - `merge_config.bat` を使用して変更を比較・統合します
   - すべてのファイルタイプをサポート: `.bat`, `.py`, `.yaml`, `.json` など

**アップデート機能:**

- ⏱️ 10秒のタイムアウト保護 (GitHubに接続できない場合でも起動をブロックしません)
- 💾 スマートな競合検出とバックアップ
- 🔄 失敗時の自動ロールバック
- 📁 バックアップのディレクトリ構造を維持

#### 🛠️ 高度なオプション

**環境検出の優先順位:**

1. `python_embeded\python.exe` (存在する場合)
2. `uv run acestep` (uvがインストールされている場合)
3. winget または PowerShell 経由での uv 自動インストール

**ダウンロードソース:**

- `auto`: 最適なソースを自動検出 (Googleへのアクセスを確認)
- `huggingface`: HuggingFace Hub を使用
- `modelscope`: ModelScope を使用

---

### 通常インストール (全プラットフォーム)

> **AMD / ROCm ユーザー:** `uv run acestep` はCUDAに最適化されており、ROCm PyTorchを上書きする可能性があります。代わりに上記の [AMD / ROCm ワークフロー](#amd--rocm-gpus) を使用してください。

### 1. uv (パッケージマネージャー) のインストール

```bash
# macOS / Linux
curl -LsSf https://astral.sh/uv/install.sh | sh

# Windows (PowerShell)
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

### 2. クローン & インストール

```bash
git clone https://github.com/ACE-Step/ACE-Step-1.5.git
cd ACE-Step-1.5
uv sync
```

### 3. 起動

#### 🖥️ Gradio Web UI (推奨)

**uv を使用する場合:**

```bash
uv run acestep
```

**Python を直接使用する場合:**

> **注意:** 最初にPython環境を有効化してください:
>
> - **Windows ポータブルパッケージ**: `python` の代わりに `python_embeded\python.exe` を使用
> - **Conda 環境**: 最初に `conda activate your_env_name` を実行
> - **venv**: 最初に `source venv/bin/activate` (Linux/Mac) または `venv\Scripts\activate` (Windows) を実行
> - **システム Python**: `python` または `python3` を直接使用

```bash
# Windows ポータブルパッケージ
python_embeded\python.exe acestep\acestep_v15_pipeline.py

# Conda/venv/システム Python
python acestep/acestep_v15_pipeline.py
```

ブラウザで http://localhost:7860 を開きます。初回実行時にモデルが自動的にダウンロードされます。

#### 🌐 REST API サーバー

**uv を使用する場合:**

```bash
uv run acestep-api
```

**Python を直接使用する場合:**

> **注意:** 最初にPython環境を有効化してください (上記の注意を参照)。

```bash
# Windows ポータブルパッケージ
python_embeded\python.exe acestep\api_server.py

# Conda/venv/システム Python
python acestep/api_server.py
```

APIは http://localhost:8001 で動作します。エンドポイントについては [API ドキュメント](./docs/en/API.md) を参照してください。

### コマンドラインオプション

**Gradio UI (`acestep`):**

| オプション          | デフォルト | 説明                                                                 |
| ------------------- | ---------- | -------------------------------------------------------------------- |
| `--port`            | 7860       | サーバーポート                                                       |
| `--server-name`     | 127.0.0.1  | サーバーアドレス (ネットワークアクセスの場合は `0.0.0.0` を使用)     |
| `--share`           | false      | 公開用Gradioリンクを作成                                             |
| `--language`        | en         | UI言語: `en`, `zh`, `he`, `ja`                                       |
| `--init_service`    | false      | 起動時にモデルを自動初期化                                           |
| `--init_llm`        | auto       | LLM 初期化: `true` (強制), `false` (無効), 省略時は自動              |
| `--config_path`     | auto       | DiTモデル (例: `acestep-v15-turbo`, `acestep-v15-turbo-shift3`)      |
| `--lm_model_path`   | auto       | LMモデル (例: `acestep-5Hz-lm-0.6B`, `acestep-5Hz-lm-1.7B`)          |
| `--offload_to_cpu`  | auto       | CPUオフロード (VRAM < 16GB の場合自動有効化)                         |
| `--download-source` | auto       | モデルダウンロードソース: `auto`, `huggingface`, または `modelscope` |
| `--enable-api`      | false      | Gradio UIと同時にREST APIエンドポイントを有効化                      |
| `--api-key`         | none       | APIエンドポイント認証用APIキー                                       |
| `--auth-username`   | none       | Gradio認証用ユーザー名                                               |
| `--auth-password`   | none       | Gradio認証用パスワード                                               |

**例:**

> **Pythonユーザー向けの注意:** `python` をお使いの環境のPython実行ファイルに置き換えてください:
>
> - Windows ポータブルパッケージ: `python_embeded\python.exe`
> - Conda: 環境を有効化してから `python` を使用
> - venv: 環境を有効化してから `python` を使用
> - システム: `python` または `python3` を使用

```bash
# 中国語UIで外部アクセスを許可
uv run acestep --server-name 0.0.0.0 --share --language zh
# Pythonを直接使用する場合:
python acestep/acestep_v15_pipeline.py --server-name 0.0.0.0 --share --language zh

# 起動時にモデルを事前初期化
uv run acestep --init_service true --config_path acestep-v15-turbo
# Pythonを直接使用する場合:
python acestep/acestep_v15_pipeline.py --init_service true --config_path acestep-v15-turbo

# 認証付きでAPIエンドポイントを有効化
uv run acestep --enable-api --api-key sk-your-secret-key --port 8001
# Pythonを直接使用する場合:
python acestep/acestep_v15_pipeline.py --enable-api --api-key sk-your-secret-key --port 8001

# Gradio認証とAPI認証の両方を有効化
uv run acestep --enable-api --api-key sk-123456 --auth-username admin --auth-password password
# Pythonを直接使用する場合:
python acestep/acestep_v15_pipeline.py --enable-api --api-key sk-123456 --auth-username admin --auth-password password

# ModelScopeをダウンロードソースとして使用
uv run acestep --download-source modelscope
# Pythonを直接使用する場合:
python acestep/acestep_v15_pipeline.py --download-source modelscope

# HuggingFace Hubをダウンロードソースとして使用
uv run acestep --download-source huggingface
# Pythonを直接使用する場合:
python acestep/acestep_v15_pipeline.py --download-source huggingface
```

### 環境変数 (.env)

`uv` または Python ユーザーの場合、`.env` ファイルを使用して ACE-Step を設定できます：

```bash
# サンプルファイルをコピー
cp .env.example .env

# .env を設定に合わせて編集
```

**主な環境変数:**

| 変数                      | 値                                  | 説明               |
| ------------------------- | ----------------------------------- | ------------------ |
| `ACESTEP_INIT_LLM`        | (空), `true`, `false`               | LLM 初期化モード   |
| `ACESTEP_CONFIG_PATH`     | モデル名                            | DiT モデルパス     |
| `ACESTEP_LM_MODEL_PATH`   | モデル名                            | LM モデルパス      |
| `ACESTEP_DOWNLOAD_SOURCE` | `auto`, `huggingface`, `modelscope` | ダウンロードソース |
| `ACESTEP_API_KEY`         | 文字列                              | API 認証キー       |

**LLM 初期化 (`ACESTEP_INIT_LLM`):**

処理フロー: `GPU 検出 (完全) → ACESTEP_INIT_LLM 上書き → モデル読み込み`

GPU 最適化 (オフロード、量子化、バッチ制限) は **常に適用されます**。上書き設定は、LLM の読み込みを試行するか、強制的に無効にするか、自動検出に任せるかを制御するだけです。

| 値                   | 動作                                                           |
| -------------------- | -------------------------------------------------------------- |
| `auto` (または空)    | GPU 自動検出の結果を使用 (推奨)                                |
| `true` / `1` / `yes` | GPU 検出後に LLM を強制的に有効化 (OOM の原因になる可能性あり) |
| `false` / `0` / `no` | 純粋な DiT モードのために強制的に無効化 (生成が高速化)         |

**シナリオ別の `.env` 例:**

```bash
# 自動モード (推奨) - GPU 検出に任せる
ACESTEP_INIT_LLM=auto

# 低 VRAM GPU で強制的に有効化 (GPU 最適化は引き続き適用されます)
ACESTEP_INIT_LLM=true
ACESTEP_LM_MODEL_PATH=acestep-5Hz-lm-0.6B

# 高速生成のために LLM を強制無効化
ACESTEP_INIT_LLM=false
```

### 開発

```bash
# 依存関係の追加
uv add package-name
uv add --dev package-name

# すべての依存関係を更新
uv sync --upgrade
```

## 🎮 その他のGPUサポート

### Intel GPU

現在、Intel GPUをサポートしています。

- **テスト済みデバイス**: Ultra 9 285H 内蔵グラフィックス搭載のWindowsラップトップ。
- **設定**:
  - `offload`（オフロード）はデフォルトで無効。
  - `compile`（コンパイル）と `quantization`（量子化）はデフォルトで有効。
- **機能**: LLM推論をサポートしています（`acestep-5Hz-lm-0.6B` でテスト済み）。
  - _注意_: 2分を超えるオーディオを生成する場合、LLM推論速度が低下する可能性があります。
  - _注意_: Intel GPUでは、LLM推論のための `nanovllm` アクセラレーションは現在サポートされていません。
- **テスト環境**: [Intel Extension for PyTorch](https://pytorch-extension.intel.com/?request=platform) の PyTorch 2.8.0。
- **Intel ディスクリート GPU**: 動作すると予想されますが、開発者がデバイスを持っていないため未テストです。コミュニティからのフィードバックをお待ちしています。

## 📥 モデルのダウンロード

`acestep` または `acestep-api` を実行すると、システムは以下を行います：

1. `./checkpoints` に必要なモデルが存在するか確認
2. 見つからない場合、設定されたソース（または自動検出）を使用して自動的にダウンロード

### CLIでの手動ダウンロード

> **Pythonユーザー向けの注意:** `python` をお使いの環境のPython実行ファイルに置き換えてください (上記の注意を参照)。

**uv を使用する場合:**

```bash
# メインモデルのダウンロード (実行に必要なすべてを含む)
uv run acestep-download

# 利用可能なすべてのモデルをダウンロード (オプションのバリエーションを含む)
uv run acestep-download --all

# ModelScope からダウンロード
uv run acestep-download --download-source modelscope

# HuggingFace Hub からダウンロード
uv run acestep-download --download-source huggingface

# 特定のモデルをダウンロード
uv run acestep-download --model acestep-v15-sft

# 利用可能なモデルを一覧表示
uv run acestep-download --list

# 指定ディレクトリにダウンロード
uv run acestep-download --dir /path/to/checkpoints
```

**Python を直接使用する場合:**

```bash
# メインモデルのダウンロード (実行に必要なすべてを含む)
python -m acestep.model_downloader

# 利用可能なすべてのモデルをダウンロード (オプションのバリエーションを含む)
python -m acestep.model_downloader --all

# ModelScope からダウンロード
python -m acestep.model_downloader --download-source modelscope

# HuggingFace Hub からダウンロード
python -m acestep.model_downloader --download-source huggingface

# 特定のモデルをダウンロード
python -m acestep.model_downloader --model acestep-v15-sft

# 利用可能なモデルを一覧表示
python -m acestep.model_downloader --list

# カスタムディレクトリにダウンロード
python -m acestep.model_downloader --dir /path/to/checkpoints
```

### huggingface-cli での手動ダウンロード

`huggingface-cli` を直接使用することも可能です：

```bash
# メインモデルのダウンロード (vae, Qwen3-Embedding-0.6B, acestep-v15-turbo, acestep-5Hz-lm-1.7B を含む)
huggingface-cli download ACE-Step/Ace-Step1.5 --local-dir ./checkpoints

# オプションのLMモデルのダウンロード
huggingface-cli download ACE-Step/acestep-5Hz-lm-0.6B --local-dir ./checkpoints/acestep-5Hz-lm-0.6B
huggingface-cli download ACE-Step/acestep-5Hz-lm-4B --local-dir ./checkpoints/acestep-5Hz-lm-4B

# オプションのDiTモデルのダウンロード
huggingface-cli download ACE-Step/acestep-v15-base --local-dir ./checkpoints/acestep-v15-base
huggingface-cli download ACE-Step/acestep-v15-sft --local-dir ./checkpoints/acestep-v15-sft
huggingface-cli download ACE-Step/acestep-v15-turbo-shift1 --local-dir ./checkpoints/acestep-v15-turbo-shift1
huggingface-cli download ACE-Step/acestep-v15-turbo-shift3 --local-dir ./checkpoints/acestep-v15-turbo-shift3
huggingface-cli download ACE-Step/acestep-v15-turbo-continuous --local-dir ./checkpoints/acestep-v15-turbo-continuous
```

### 利用可能なモデル

| モデル                       | HuggingFace リポジトリ                                                                                | 説明                                                                                  |
| ---------------------------- | ----------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| **Main**                     | [ACE-Step/Ace-Step1.5](https://huggingface.co/ACE-Step/Ace-Step1.5)                                   | コアコンポーネント: vae, Qwen3-Embedding-0.6B, acestep-v15-turbo, acestep-5Hz-lm-1.7B |
| acestep-5Hz-lm-0.6B          | [ACE-Step/acestep-5Hz-lm-0.6B](https://huggingface.co/ACE-Step/acestep-5Hz-lm-0.6B)                   | 軽量LMモデル (0.6B params)                                                            |
| acestep-5Hz-lm-4B            | [ACE-Step/acestep-5Hz-lm-4B](https://huggingface.co/ACE-Step/acestep-5Hz-lm-4B)                       | 大規模LMモデル (4B params)                                                            |
| acestep-v15-base             | [ACE-Step/acestep-v15-base](https://huggingface.co/ACE-Step/acestep-v15-base)                         | ベースDiTモデル                                                                       |
| acestep-v15-sft              | [ACE-Step/acestep-v15-sft](https://huggingface.co/ACE-Step/acestep-v15-sft)                           | SFT DiTモデル                                                                         |
| acestep-v15-turbo-shift1     | [ACE-Step/acestep-v15-turbo-shift1](https://huggingface.co/ACE-Step/acestep-v15-turbo-shift1)         | Turbo DiT (shift1)                                                                    |
| acestep-v15-turbo-shift3     | [ACE-Step/acestep-v15-turbo-shift3](https://huggingface.co/ACE-Step/acestep-v15-turbo-shift3)         | Turbo DiT (shift3)                                                                    |
| acestep-v15-turbo-continuous | [ACE-Step/acestep-v15-turbo-continuous](https://huggingface.co/ACE-Step/acestep-v15-turbo-continuous) | Turbo DiT (continuous shift 1-5)                                                      |

### 💡 どのモデルを選ぶべき？

ACE-StepはGPUのVRAMに合わせて自動的に適応します。簡易ガイドはこちら：

| あなたのGPU VRAM | 推奨LMモデル          | メモ                                 |
| ---------------- | --------------------- | ------------------------------------ |
| **≤6GB**         | なし (DiTのみ)        | メモリ節約のためLMはデフォルトで無効 |
| **6-12GB**       | `acestep-5Hz-lm-0.6B` | 軽量、バランス良好                   |
| **12-16GB**      | `acestep-5Hz-lm-1.7B` | より高品質                           |
| **≥16GB**        | `acestep-5Hz-lm-4B`   | 最高品質とオーディオ理解能力         |

> 📖 **詳細なGPU互換性情報**（長さ制限、バッチサイズ、メモリ最適化）については、GPU互換性ガイドを参照してください： [English](./docs/en/GPU_COMPATIBILITY.md) | [中文](./docs/zh/GPU_COMPATIBILITY.md) | [日本語](./docs/ja/GPU_COMPATIBILITY.md)

## 🚀 使い方

ACE-Stepを使用するには複数の方法があります：

| 方法                      | 説明                                                     | ドキュメント                              |
| ------------------------- | -------------------------------------------------------- | ----------------------------------------- |
| 🖥️ **Gradio Web UI**      | 音楽生成のためのインタラクティブなWebインターフェース    | [Gradio Guide](./docs/en/GRADIO_GUIDE.md) |
| 🎚️ **Studio UI (実験的)** | REST API用のオプションのHTMLフロントエンド (DAW風)       | [Studio UI](./docs/en/studio.md)          |
| 🐍 **Python API**         | 統合のためのプログラムからのアクセス                     | [Inference API](./docs/en/INFERENCE.md)   |
| 🌐 **REST API**           | サービス向けのHTTPベース非同期API                        | [REST API](./docs/en/API.md)              |
| ⌨️ **CLI**                | コマンドラインインターフェース用の対話型ウィザードと設定 | [CLI Guide](./docs/en/CLI.md)             |

**📚 ドキュメント言語:** [English](./docs/en/) | [中文](./docs/zh/) | [日本語](./docs/ja/)

## 📖 チュートリアル

### 実験的 Studio UI

より構造化されたインターフェースを好むユーザー向けに、オプションのフロントエンドのみの HTML Studio UI が利用可能です。これは同じ REST API を使用し、バックエンドの動作を変更しません。API サーバーを起動し、ブラウザで `ui/studio.html` を開き、API URL を指定してください。[Studio UI](./docs/en/studio.md) を参照してください。

### チュートリアル

| 言語       | リンク                                        |
| ---------- | --------------------------------------------- |
| 🇺🇸 English | [English Tutorial](./docs/en/Tutorial.md)     |
| 🇨🇳 中文    | [中文教程](./docs/zh/Tutorial.md)             |
| 🇯🇵 日本語  | [日本語チュートリアル](./docs/ja/Tutorial.md) |

このチュートリアルでは以下をカバーしています：

- メンタルモデルと設計思想
- モデルアーキテクチャと選択
- 入力制御 (テキストおよびオーディオ)
- 推論ハイパーパラメータ
- ランダム要素と最適化戦略

## 🔨 学習

Gradio UIの **LoRA Training** タブでワンクリック学習を行うか、詳細は [Gradio Guide - LoRA Training](./docs/en/GRADIO_GUIDE.md#lora-training) を確認してください。

## 🏗️ アーキテクチャ

<p align="center">
    <img src="./assets/ACE-Step_framework.png" width="100%" alt="ACE-Step Framework">
</p>

## 🦁 モデル Zoo

<p align="center">
    <img src="./assets/model_zoo.png" width="100%" alt="Model Zoo">
</p>

### DiT モデル

| DiT モデル             | 事前学習 | SFT | RL  | CFG | ステップ数 | 音声参照 | Text2Music | カバー | リペイント | 抽出 | Lego | 補完 |    品質    | 多様性 | 微調整 | Hugging Face                                             |
| ---------------------- | :------: | :-: | :-: | :-: | :--------: | :------: | :--------: | :----: | :--------: | :--: | :--: | :--: | :--------: | :----: | :----: | -------------------------------------------------------- |
| `acestep-v15-base`     |    ✅    | ❌  | ❌  | ✅  |     50     |    ✅    |     ✅     |   ✅   |     ✅     |  ✅  |  ✅  |  ✅  |     中     |   高   |  容易  | [Link](https://huggingface.co/ACE-Step/acestep-v15-base) |
| `acestep-v15-sft`      |    ✅    | ✅  | ❌  | ✅  |     50     |    ✅    |     ✅     |   ✅   |     ✅     |  ❌  |  ❌  |  ❌  |     高     |   中   |  容易  | [Link](https://huggingface.co/ACE-Step/acestep-v15-sft)  |
| `acestep-v15-turbo`    |    ✅    | ✅  | ❌  | ❌  |     8      |    ✅    |     ✅     |   ✅   |     ✅     |  ❌  |  ❌  |  ❌  | 非常に高い |   中   |  普通  | [Link](https://huggingface.co/ACE-Step/Ace-Step1.5)      |
| `acestep-v15-turbo-rl` |    ✅    | ✅  | ✅  | ❌  |     8      |    ✅    |     ✅     |   ✅   |     ✅     |  ❌  |  ❌  |  ❌  | 非常に高い |   中   |  普通  | 近日公開                                                 |

### LM モデル

| LM モデル             | ベースモデル | 事前学習 | SFT | RL  | CoT メタ | クエリ書き換え | オーディオ理解 | 作曲能力 | メロディコピー | Hugging Face |
| --------------------- | ------------ | :------: | :-: | :-: | :------: | :------------: | :------------: | :------: | :------------: | ------------ |
| `acestep-5Hz-lm-0.6B` | Qwen3-0.6B   |    ✅    | ✅  | ✅  |    ✅    |       ✅       |       中       |    中    |      弱い      | ✅           |
| `acestep-5Hz-lm-1.7B` | Qwen3-1.7B   |    ✅    | ✅  | ✅  |    ✅    |       ✅       |       中       |    中    |      普通      | ✅           |
| `acestep-5Hz-lm-4B`   | Qwen3-4B     |    ✅    | ✅  | ✅  |    ✅    |       ✅       |       強       |    強    |      強い      | ✅           |

## 📜 ライセンス & 免責事項

本プロジェクトは [MIT](./LICENSE) ライセンスの下で提供されています。

ACE-Stepは、多様なジャンルにわたるオリジナルの音楽生成を可能にし、クリエイティブな制作、教育、エンターテインメントへの応用が可能です。肯定的かつ芸術的な使用事例をサポートするように設計されていますが、スタイルの類似性による意図しない著作権侵害、文化的要素の不適切な混合、有害なコンテンツの生成への悪用などの潜在的なリスクを認識しています。責任ある使用を保証するため、ユーザーには生成された作品のオリジナリティを確認し、AIの関与を明確に開示し、保護されたスタイルや素材を採用する場合は適切な許可を得ることを推奨します。ACE-Stepを使用することで、これらの原則を支持し、芸術的完全性、文化的多様性、法的コンプライアンスを尊重することに同意したものとみなされます。著者は、著作権侵害、文化的無神経さ、または有害なコンテンツの生成を含むがこれらに限定されない、モデルの悪用について一切の責任を負いません。

🔔 重要なお知らせ  
ACE-Stepプロジェクトの唯一の公式サイトはGitHub Pagesサイトのみです。  
私たちは他のいかなるウェブサイトも運営していません。  
🚫 偽ドメインの例：
ac**p.com, a**p.org, a\*\*\*c.org  
⚠️ ご注意ください。これらのサイトにアクセスしたり、信頼したり、支払いをしたりしないようにしてください。

## 🙏 謝辞

このプロジェクトは、ACE StudioとStepFunによって共同主導されています。

## 📖 引用

本プロジェクトが研究に役立つ場合は、引用をお願いします：

```BibTeX
@misc{gong2026acestep,
	title={ACE-Step 1.5: Pushing the Boundaries of Open-Source Music Generation},
	author={Junmin Gong, Yulin Song, Wenxiao Zhao, Sen Wang, Shengyuan Xu, Jing Guo},
	howpublished={\url{https://github.com/ace-step/ACE-Step-1.5}},
	year={2026},
	note={GitHub repository}
}
```
