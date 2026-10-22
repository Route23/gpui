# gpui 0.2.2 — Route23 の fork

[dopamine](https://github.com/Route23/dopamine) が `[patch.crates-io]` で差し替えるための、crates.io の `gpui 0.2.2` の写し。

- 最初のコミットは crates.io のパッケージそのもの（`cargo package` の中身）
- 2 つめ以降が dopamine の直し。どれも上流（zed-industries/zed）に同じ直しがあり、crates.io に出ていないものだけ
- 何を当てているかは dopamine の ADR-0062 の表が正典

| 直し | 上流 |
|---|---|
| 画面の構成が変わったとき、`screen` が nil の窓で `display_id_for_screen` を撃って落ちない | zed-industries/zed#60419 |
