# gpui 0.2.2 — Route23 の fork

[dopamine](https://github.com/Route23/dopamine) が `[patch.crates-io]` で差し替えるための、crates.io の `gpui 0.2.2` の写し。

- 最初のコミットは crates.io のパッケージそのもの（`cargo package` の中身）
- 2 つめ以降が dopamine の直し。どれも上流（zed-industries/zed）に同じ直しがあり、crates.io に出ていないものだけ
- 何を当てているかは dopamine の ADR-0062 の表が正典

| 直し | 上流 |
|---|---|
| 画面の構成が変わったとき、`screen` が nil の窓で `display_id_for_screen` を撃って落ちない | zed-industries/zed#60419 |
| アクセシビリティの木（AccessKit）。要素に `.role()` / `.aria_label()` などを付けると、VoiceOver が読み・押せる。**既定 off**（`gpui::set_accessibility_enabled(true)` を窓を作る前に呼んだときだけ）。mac は `GPUIView` に `accesskit_macos::Adapter` を付け、子にネイティブの subview（WKWebView）も残す | zed-industries/zed#56065（mac の部分は 0.2.2 の一枚岩の `platform/mac/window.rs` に合わせて書き直し。`Text` 要素の分は外した） |
| アクセシビリティの木の続き: キャッシュしたビュー（`AnyView::cached`）は木を作っている間は使い回さない（使い回したフレームの中の要素が木から消える）・押せる役割（ボタン・スイッチ・タブ…）は自分で受けなくても「押せる」・`aria_value` / `aria_description` | dopamine の手当て（Route23/dopamine#1286） |
| 試しの引き金（debug だけ）: `GPUI_SIMULATE_DEVICE_LOST_SECS=N` で N 秒ごとに「DirectX のデバイスを失った」ことにして作り直しの道を走らせる（Windows） | dopamine の手当て（Route23/dopamine#1133） |
| App を借りている最中に来た窓の知らせ（動いた・大きさ・外観・前面・ホバー）を捨てず、借りが返ってから 1 回やり直す | dopamine の手当て（Route23/dopamine#1295） |
