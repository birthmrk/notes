# AIがソースコードから AI 理解用ドキュメントを生成する最適アプローチ

## 基本戦略：階層化プロンプト設計

**AIが理解しやすいドキュメント** を生成するには、以下3つの要素を意識したプロンプト設計が重要です

1. **構造化された出力形式の指定**
2. **役割と文脈の明確化** 
3. **段階的な情報抽出**

## 効果的なプロンプトパターン

### 1. 基本テンプレート

```
役割: あなたは AI システム向けの技術ドキュメント生成の専門家です。

タスク: 以下のソースコードから、AIが理解・処理しやすい構造化ドキュメントを生成してください。

出力形式: 
- 目的と機能の要約
- 入力・出力の型定義
- 主要アルゴリズムの説明
- 依存関係の明示
- 使用例とテストケース

制約:
- 技術的精度を最優先する
- 曖昧な表現を避ける
- JSON Schema や型定義を含める

[ソースコード]
```

### 2. 段階的分析プロンプト

**Step 1: 構造解析**
```
このコードの構造を以下の形式で分析してください：
- クラス/関数一覧: [名前, 責務, 依存関係]
- データフロー: [入力→処理→出力]
- 例外処理: [エラーケースと対処法]
```

**Step 2: 機能説明**
```
各関数について以下を生成してください：
- 目的: 何をするか（1文で）
- パラメータ: 型と説明
- 戻り値: 型と意味
- 副作用: ファイル操作、状態変更など
- 計算量: 時間/空間計算量（該当する場合）
```

### 3. AI理解特化プロンプト

```
以下のコードを Machine Learning / AI システムが理解・利用しやすい形式でドキュメント化してください：

重点項目:
1. 型情報を明示的に記載
2. 入出力の次元・形状を数値で表現
3. アルゴリズムの数学的根拠を含める
4. パフォーマンス特性（メモリ使用量、実行時間）を記載
5. 設定可能パラメータのデフォルト値と推奨範囲

出力形式: JSON + Markdown のハイブリッド構造
```

## 具体的な実装例

### コード解析用プロンプト

```
Act as a code documentation specialist for AI systems.

Analyze this code and generate comprehensive documentation that includes:

**Functional Specification:**
- Purpose: [One-line summary]
- Input Contract: [Type definitions with constraints]  
- Output Contract: [Return types with examples]
- Side Effects: [State changes, I/O operations]

**Implementation Details:**
- Algorithm: [Step-by-step logic explanation]
- Complexity: [Time/Space complexity in Big O notation]
- Dependencies: [External libraries and internal modules]

**Usage Patterns:**
- Success Cases: [2-3 working examples with expected outputs]
- Error Cases: [Common failure modes and error handling]
- Performance Notes: [Memory usage, execution time estimates]

Format the output as structured JSON where possible for machine readability.

[SOURCE CODE HERE]
```

## 段階的アプローチ

1. **粗い解析**: 全体構造の把握[1]
2. **詳細分析**: 個別コンポーネントの機能[3]
3. **関連性マッピング**: モジュール間の依存関係[2]
4. **検証**: 生成されたドキュメントの妥当性チェック

この手法により、AIがコードの意図を正確に理解し、後続のタスク（コード生成、バグ検出、リファクタリング提案など）で活用できる高品質なドキュメントが生成できます。[4][5]
