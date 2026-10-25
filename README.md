# 日本語Colabノートブック集

画像と音声から話す人物・キャラクターの動画を作成する、Google Colab向けの日本語ノートブック集です。InfiniteTalk、MiniMax H3、H3＋LatentSyncを用途別にまとめています。

## ノートブックを選ぶ

リンク先のノートブック冒頭にある説明と、番号付きセルの順序に沿って実行してください。下表のGPUは各ノートブックが想定する環境です。

| ノートブック | 用途・主な機能 | 想定GPU | Colab |
| --- | --- | --- | --- |
| [InfiniteTalk v10](notebooks/infinitetalk/InfiniteTalk_G4_Fast_ResultsTable_JP_v10.ipynb) | 画像＋音声から動画生成。音声長の自動検出、生成時間の結果表、MP4・レポートのZIP出力 | G4を想定。安定版・省VRAMモードあり | [開く](https://colab.research.google.com/github/dma-cmyk/colab/blob/main/notebooks/infinitetalk/InfiniteTalk_G4_Fast_ResultsTable_JP_v10.ipynb) |
| [MiniMax H3 Ref2VA v5](notebooks/minimax-h3/MiniMax_H3_Ref2VA_Colab_JP_v5_FullAudio_Fix.ipynb) | 画像・音声を参照して短い動画を生成。4／8／20ステップ切替、元音声との比較版を出力 | A100 40GB／80GB・G4を想定 | [開く](https://colab.research.google.com/github/dma-cmyk/colab/blob/main/notebooks/minimax-h3/MiniMax_H3_Ref2VA_Colab_JP_v5_FullAudio_Fix.ipynb) |
| [H3＋LatentSync v14.1](notebooks/h3-latentsync/H3_LatentSync_Universal_A100_v14_1_MultiRef_Fix_Resume_JP.ipynb) | **最新版（実GPU未検証）**。音声全尺から分割数を自動計算。MultiRef Motion Contextでクリップ間を引き継ぎ、元画像への定期リセットで顔の変化を抑える設定、途中再開、LatentSync比較に対応。Context LoopのPlan Studioを使う完全移行版ではない | A100を想定 | [開く](https://colab.research.google.com/github/dma-cmyk/colab/blob/main/notebooks/h3-latentsync/H3_LatentSync_Universal_A100_v14_1_MultiRef_Fix_Resume_JP.ipynb) |
| [H3＋LatentSync v12](notebooks/h3-latentsync/H3_LatentSync_Universal_A100_v12_Japanese_Guide.ipynb) | **旧版**。H3で体・表情を生成し、LatentSyncで元音声に合わせて口元を修正。既存動画の利用、分割・結合、設定比較に対応 | A100を想定 | [開く](https://colab.research.google.com/github/dma-cmyk/colab/blob/main/notebooks/h3-latentsync/H3_LatentSync_Universal_A100_v12_Japanese_Guide.ipynb) |

**掲載版がすべて実GPUで動作確認済みという意味ではありません。** InfiniteTalk v10とH3＋LatentSync v12／v14.1は、その版の実GPU動作が未確認です。v14.1はMultiRef入力エラーの修正後、A100での2本目以降の正常生成をまだ確認していません。MiniMax H3 v5の8ステップも実験モードです。まず短い素材で結果を確認してください。

InfiniteTalkの旧版は[旧版一覧](notebooks/infinitetalk/archive/README.md)に残しています。版番号は各系統内の番号で、異なるモデル間の性能順位を示すものではありません。

## はじめ方

1. 上の表からノートブックを選び、「開く」でColabへ移動します。必要なら自分のGoogle Driveへコピーして使用します。
2. ノートブックの説明を読み、Colabの **［ランタイム］→［ランタイムのタイプを変更］** で想定GPUを選択します。
3. ノートブックの番号順にセルを実行し、画像・音声をアップロードして生成条件を設定します。旧版とはセルの順序が異なります。
4. 初回は短時間のテストを行います。InfiniteTalk v10は `TEST_FIRST_SECONDS=5`、H3系は `TEST_SECONDS=5` が設定例です。どちらも `0` は音声全体を使用する設定です。
5. 最後の出力セルから、完成MP4・レポート・ZIPなどを手元に保存します。

初回の環境構築・モデル取得には時間とディスク容量が必要です。ノートブックがColab内に依存関係を導入するため、このリポジトリをローカルにcloneして実行する必要はありません。

## フォルダ構成

```text
.
├── README.md
├── .gitignore
└── notebooks/
    ├── infinitetalk/
    │   ├── InfiniteTalk_G4_Fast_ResultsTable_JP_v10.ipynb
    │   └── archive/          # v4・v5・v7・v9と旧版一覧
    ├── minimax-h3/
    │   └── MiniMax_H3_Ref2VA_Colab_JP_v5_FullAudio_Fix.ipynb
    └── h3-latentsync/
        ├── H3_LatentSync_Universal_A100_v12_Japanese_Guide.ipynb
        └── H3_LatentSync_Universal_A100_v14_1_MultiRef_Fix_Resume_JP.ipynb
```

整理に伴い、従来ルートに置いていたノートブックを上記のフォルダへ移動しました。MiniMax H3のファイル名末尾にあった ` (1)` も取り除いています。旧URLやブックマークを使っている場合は、上の表のリンクへ更新してください。ノートブック本体の内容は移動前から変更していません。

## 実行時の注意

- **GPU・費用**：利用可能なGPUはColab側の状況によります。モデル取得中もGPU接続時間を消費するため、利用枠を確認して実行してください。
- **一時保存**：入力素材や生成物は主にColabの `/content` 配下へ保存されます。ランタイムの削除などで失われるため、必要な成果物はダウンロードしてください。
- **MiniMax H3の音声**：Ref2VAは音声を参照に使う方式で、元の日本語音声の発話やタイミングを完全に再現する保証はありません。v5は生成映像の上限が約14.38秒で、元音声比較版では不足する映像を静止延長します。
- **H3＋LatentSyncの長尺生成（v14.1）**：音声長に合わせて分割・生成・結合します。定期的な元画像への再アンカーにより顔の変化を抑えることを狙いますが、再アンカー地点で動きが途切れる可能性があります。Context Loop本体のプロジェクト管理・Plan Studio・Loop Start/Endを実行する完全なContext Loopワークフローではなく、関連するMultiRef Motion Contextノードを用いた自動生成方式です。MultiRef修正後のA100実推論は未検証です。
- **H3＋LatentSyncの分割処理**：長い素材は分割・結合します。音声と動画の尺が一致していても、口パクの正確さや区間をまたぐ動きの連続性は、再生して確認する必要があります。
- **実行環境の変化**：各ノートブックが取得する外部コード・モデル・依存パッケージの変更により、動作が変わる場合があります。エラー時は実行セルとログを確認してください。

## 追加・更新するとき

- ノートブックは `notebooks/<モデル名>/` に置き、日本語の用途説明、想定GPU、実行順、検証状況を冒頭に記載してください。
- 旧版を比較用に残す場合は、その系統の `archive/` に移し、一覧とColabリンクを更新してください。
- コミット前に実行結果・個人情報・認証トークンを確認し、不要な出力を消してください。素材、生成動画、モデル重み、ログはリポジトリへ含めない運用です。
- JSON形式とコードセルの構文確認に加え、実GPUで確認した範囲と未確認の範囲を区別してください。

モデルや依存コード、入力素材の利用条件はそれぞれの配布元・権利者の条件に従ってください。このリポジトリで第三者のモデル等に新たな利用許諾を与えるものではありません。
