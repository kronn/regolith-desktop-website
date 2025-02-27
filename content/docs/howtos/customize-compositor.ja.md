---
title: "コンポジターのカスタマイズ"
linkTitle: "コンポジターのカスタマイズ"
description: >
  Regolithのコンポジターをカスタマイズする方法
---

# コンポジターをカスタマイズする方法（仮想エフェクト）

{{< hint info >}}
異常な視覚的不具合やグラフィックパフォーマンスの低下を経験している場合は、
このセクションに特に注意してください。
{{< /hint >}}

コンポジターは、ウィンドウをスクリーンに表示するときに仮想エフェクトを適用するUIコンポーネントです。
いくつかのデスクトップ環境ではコンポジターがウィンドウマネージャーに直接統合されており、
仮想エフェクトを切り替えたり無効にすることができます。
Regolithでは、コンポジターはパッケージングシステムで繋ぎ変え可能な“extension point”として定義されます。
これは、コンポジターを含むパッケージをインストールすることでコンポジターを切り替えることができるということを意味します。
基礎となるパッケージングシステムは競合が起きないことを確認し、
コンポジターを含めたすべての依存関係が
インストールされていることを確認してください。

{{< hint warning >}}
警告：Regolith 2.xでは、既定のコンポジターは"コンポジターなし"です。
Regolith 1.xでは、既定のコンポジターはPicomでした。
{{< /hint >}}

## 利用可能なコンポジターを探す

Regolithで動作するすべてのコンポジター設定は、
以下のコマンドで一覧表示されます：

```console
apt search regolith-compositor-
```

以下の項目を見つけることができます：

- `regolith-compositor-none` **[既定]**：コンポジターなし。
最高のパフォーマンス、仮想エフェクトなし。
- `regolith-compositor-picom-glx`：`picom`を使用します。
画面のつなぎ目の解決や仮想エフェクトの追加するとき、多くのユーザーに推奨されます。`compton`からフォークされ、モダンで管理されています。
Regolith 1.6の既定のコンポジターでした。
- `regolith-compositor-compton-glx`：既にメンテナンスされていない、
`picom`の祖先です。
- `regolith-compositor-xcompmgr`：初期のコンポジターで、より複雑なコンポジターに問題がある場合、
より安定したパフォーマンスを提供する可能性があります。

## コンポジターのインストール

{{< hint info >}}
i3-wmでコンポジターを管理する方法により、**コンポジターの変更をエフェクトに適用するため、
ログアウトしてから戻る必要があります**。
i3の再起動では代替できません。
{{< /hint >}}

次のパッケージインストールコマンドを実行して、コンポジターを交換します。
`picom`をインストールする場合：

```console
apt install regolith-compositor-picom
```

**一度ログアウトして戻ってから**新しいコンポジターを読み込みます。
プロセスのリストから`picom`が動作していることを確認することができます：

```console
ps aux | grep picom
```

## Regolithの既定のコンポジター設定のオーバーライド

### Compton/Picom

独自のCompton/Picomコンポジターの設定を提供するには、
既定値をコピーするか独自に用意し、`~/.config/regolith3/picom/config`に保存します。
次のセッションでは、既定の設定である`/etc/regolith/picom/config`の代わりに
読み込まれます。
