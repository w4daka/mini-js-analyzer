# Ticket 1: Cargoプロジェクト作成

## Goal

`mini-js-analyzer`の学習開発を開始するため、最小のRust/Cargoプロジェクトを作成する。

このチケットではAST、Parser、Lexerなどの実装は行わず、今後のチケットで実装と検証を繰り返せる最小の開発基盤だけを作る。

## Scope

### In Scope

- Cargoプロジェクトの作成
- `src/main.rs`の確認
- `Cargo.toml`の確認
- CargoによるBuild / Test / Runの確認
- Cargoプロジェクトの基本構造の理解

### Out of Scope

- ASTの実装
- Parserの実装
- Lexerの実装
- Visitorの実装
- JavaScriptの解析

## Initial Design

最初はプロジェクトを最小構成にする。

```text
mini-js-analyzer/
├── Cargo.toml
└── src/
    └── main.rs
```

将来的に`ast.rs`や`parser.rs`などが必要になる可能性はあるが、現時点では作成しない。

理由は、まだ必要になっていない構造を先に作るのではなく、要求と責務に応じて必要になった時点で構造を追加するためである。

## Key Decisions

### 1. `src/main.rs`をエントリーポイントとして使用する

`main.rs`は実行可能プログラムの入口として扱う。

### 2. `Cargo.toml`をプロジェクトのマニフェストとして使用する

`Cargo.toml`にはプロジェクトに関する設定や依存関係などを記述する。

### 3. 最初からモジュールを過剰に分割しない

`ast.rs`、`parser.rs`、`lexer.rs`などを最初から作成せず、必要になった段階で分離する。

これは「特定のファイル構成を守る」ためではなく、責務や変更理由に応じて構造を決定するためである。

## Verification

以下のCargo操作を使用してプロジェクトを検証する。

```text
cargo build
cargo test
cargo run
```

それぞれ、

- `cargo build`: プロジェクトをビルドする
- `cargo test`: テストを実行する
- `cargo run`: 必要に応じてビルドしたうえでプログラムを実行する

という役割を確認した。

## Learning Result

今回確認した主な内容は以下。

### `src/main.rs`

実行可能プログラムのエントリーポイント。

### `Cargo.toml`

Cargoプロジェクトのマニフェスト。

依存関係だけでなく、プロジェクトに関する設定も記述する。

### Cargo

RustプロジェクトのBuild / Test / Runなどを管理する。

## Design Understanding

`main.rs`にASTやParserなどをすべて実装することも技術的には可能だが、役割の異なるコードを一箇所に集めると責務が増える。

一方で、最初からすべてを別ファイルに分割する必要もない。

したがって、

```text
現在必要なもの
    ↓
最小実装
    ↓
新しい要求
    ↓
必要になった構造を追加
```

という方針を採用する。

これは「ASTだから`ast.rs`」「Parserだから`parser.rs`」という固定規則ではなく、責務と変更理由に基づいて構造を決定するという設計上の判断である。

## Learning Assessment

Ticket 1では、以下を説明できることを確認した。

- `main.rs`がエントリーポイントである
- `Cargo.toml`がCargoプロジェクトのマニフェストである
- `cargo build`がビルドを行う
- `cargo run`がプログラムを実行する
- `main.rs`に異なる責務を過剰に集中させない方がよい
- ただし、責務が違うという理由だけで必ず別ファイルに分割するわけではない

## Status

**Accepted**

Ticket 1の理解確認を完了した。

次の学習対象はRustの`enum`と、それを利用した最小ASTの表現とする。
