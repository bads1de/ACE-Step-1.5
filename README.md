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

### 🪟 Windows ポータブルパッケージ (Windows 推奨)

Windowsユーザー向けに、依存関係がインストール済みのポータブルパッケージを提供しています：

1. ダウンロードして解凍: [ACE-Step-1.5.7z](https://files.acemusic.ai/acemusic/win/ACE-Step-1.5.7z)
2. パッケージにはすべての依存関係が含まれた `python_embeded` が同梱されています
3. **要件:** CUDA 12.8

**起動:**

```bash
# Gradio Web UI
python_embeded\python -m acestep.entry.gradio_app

# REST API サーバー
python_embeded\python -m acestep.entry.api_server
```

---

### 通常インストール (全プラットフォーム)

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

```bash
uv run acestep
```

ブラウザで http://localhost:7860 を開きます。初回実行時にモデルが自動的にダウンロードされます。

#### 🌐 REST API サーバー

```bash
uv run acestep-api
```

APIは http://localhost:8001 で動作します。エンドポイントについては [API ドキュメント](./docs/en/API.md) を参照してください。

### コマンドラインオプション

**Gradio UI (`acestep`):**

| オプション         | デフォルト | 説明                                                             |
| ------------------ | ---------- | ---------------------------------------------------------------- |
| `--port`           | 7860       | サーバーポート                                                   |
| `--server-name`    | 127.0.0.1  | サーバーアドレス (ネットワークアクセスの場合は `0.0.0.0` を使用) |
| `--share`          | false      | 公開用Gradioリンクを作成                                         |
| `--language`       | en         | UI言語: `en`, `zh`, `ja`                                         |
| `--init_service`   | false      | 起動時にモデルを自動初期化                                       |
| `--config_path`    | auto       | DiTモデル (例: `acestep-v15-turbo`, `acestep-v15-turbo-shift3`)  |
| `--lm_model_path`  | auto       | LMモデル (例: `acestep-5Hz-lm-0.6B`, `acestep-5Hz-lm-1.7B`)      |
| `--offload_to_cpu` | auto       | CPUオフロード (VRAM < 16GB の場合自動有効化)                     |
| `--enable-api`     | false      | Gradio UIと同時にREST APIエンドポイントを有効化                  |
| `--api-key`        | none       | APIエンドポイント認証用APIキー                                   |
| `--auth-username`  | none       | Gradio認証用ユーザー名                                           |
| `--auth-password`  | none       | Gradio認証用パスワード                                           |

**例:**

```bash
# 中国語UIで外部アクセスを許可
uv run acestep --server-name 0.0.0.0 --share --language zh

# 起動時にモデルを事前初期化
uv run acestep --init_service true --config_path acestep-v15-turbo

# 認証付きでAPIエンドポイントを有効化
uv run acestep --enable-api --api-key sk-your-secret-key --port 8001

# Gradio認証とAPI認証の両方を有効化
uv run acestep --enable-api --api-key sk-123456 --auth-username admin --auth-password password
```

### 開発

```bash
# 依存関係の追加
uv add package-name
uv add --dev package-name

# すべての依存関係を更新
uv sync --upgrade
```

## 📥 モデルのダウンロード

モデルは初回実行時に [HuggingFace](https://huggingface.co/ACE-Step/Ace-Step1.5) または [ModelScope](https://modelscope.cn/organization/ACE-Step) から自動的にダウンロードされます。CLIまたは `huggingface-cli` を使用して手動でダウンロードすることも可能です。

### 自動ダウンロード

`acestep` または `acestep-api` を実行すると、システムは以下を行います：

1. `./checkpoints` に必要なモデルが存在するか確認
2. 見つからない場合、HuggingFaceから自動的にダウンロード

### CLIでの手動ダウンロード

```bash
# メインモデルのダウンロード (実行に必要なすべてを含む)
uv run acestep-download

# 利用可能なすべてのモデルをダウンロード (オプションのバリエーションを含む)
uv run acestep-download --all

# 特定のモデルをダウンロード
uv run acestep-download --model acestep-v15-sft

# 利用可能なモデルを一覧表示
uv run acestep-download --list

# 指定ディレクトリにダウンロード
uv run acestep-download --dir /path/to/checkpoints
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

| 方法                 | 説明                                                  | ドキュメント                              |
| -------------------- | ----------------------------------------------------- | ----------------------------------------- |
| 🖥️ **Gradio Web UI** | 音楽生成のためのインタラクティブなWebインターフェース | [Gradioガイド](./docs/en/GRADIO_GUIDE.md) |
| 🐍 **Python API**    | 統合のためのプログラムからのアクセス                  | [推論 API](./docs/en/INFERENCE.md)        |
| 🌐 **REST API**      | サービス向けのHTTPベース非同期API                     | [REST API](./docs/en/API.md)              |

**📚 ドキュメント言語:** [English](./docs/en/) | [中文](./docs/zh/) | [日本語](./docs/ja/)

## 📖 チュートリアル

**🎯 必読:** ACE-Step 1.5の設計思想と使用方法に関する包括的なガイドです。

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
ac\*\*p.com, a\*\*p.org, a\*\*\*c.org  
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
