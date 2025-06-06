# Homework[3]
WEBページなどの履歴管理におけるキャッシュ管理をほぼO(1)で実装できるデータ構造を考える
## 考え方
目標：「もっとも直近にアクセスされた上位 X 個の <URL, Web ページ> の組が保存できるデータ構造」を作ればよい

以下の操作がほぼ O(1) で実現できるようなデータ構造を考える
与えられた <URL, Web ページ> があるかないかを検索
もしない場合、キャッシュ内で一番古い <URL, Web ページ> を捨てて、代わりに与えられた <URL, Web ページ> を追加する
また、ハッシュテーブルだけだと順序を管理できないので、別のデータ構造を組み合わせて、X 個の <URL, Web ページ> をアクセスされた順に取り出せるようにする
## Answer
linked listとハッシュテーブルを組み合わせる。計算量としてlinked listは先頭へのアクセス:O(1), 一番後ろはo(N)、hashはデータの検索・追加・削除ともにO(1)
長さを固定したlinked listを作り、それぞれの要素を繋げることで参照順序を管理する。
1. 参照した要素を入れるときリスト内が空いている場合、そのまま追加する：O(1）
2. 参照した要素がリスト内にない場合、その要素を先頭に追加しリスト内の一番後ろの要素を削除:O(1)
3. 参照した要素がリスト内にある場合、その要素を先頭に追加しリスト内にある同じ要素の前後にアクセスし繋ぎ直す：O(1)
以上よりキャッシュ管理をほぼO(1)で実装が可能。
