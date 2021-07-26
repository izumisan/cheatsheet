# Quaternion(四元数)

- 1つの実部と3つの虚部で表現される
    - xi + yj + zk + w
    - (x, y, z, w)
        - 実部wが最初に記載される例もある -> (w, x, y, z)
- 方向ベクトル(λx, λy, λz)に対し、角度θだけ回転するクォータ二オン
    - (λxsin(θ/2), λysin(θ/2), λzsin(θ/2), cos(θ/2))
- 3Dライブラリや航空業界におけるクォータニオンのノルムは暗黙的に1であるという制約が多い
    - 敢えて言うなら回転クォータニオン...(ほとんど聞かない)
- 共役クォータニオン($q^*$や$\overline{q}$で表されることが多い)による回転は、逆回転を示す
    - 共役クォータニオン: 虚部の符号が反転
    - (-x, -y, -z, w)
- 逆クォータニオン(逆数)($q^{-1}$)による回転は、元のクォータニオンによる回転と同じ
    - e.g. +Z軸回りに+θ回転と-Z軸周りに-θ回転は同じ
    - 逆クォータニオン: 掛けたら1になるクォータニオン(全要素の符号が逆)
        - $ q q^{-1} = q^{-1} q = 1 $
    - (-x, -y, -z, -w)
- 逆クォータニオンは、共役クォータニオンを使って求めることができる
    - $ q^{-1} = q^* / |q^2| $
- クォータニオンq1で回転した後、クォータニオンq2で回転 = クォータニオン q2q1 による回転
- クォータニオンとベクトルの掛け算
    - $q\vec{v}\overline{q}$
    - 大体のライブラリでは、`q*v`と書けば、内部的に上記の演算をしてくれる($\overline{q}$成分は不要)

# 参考

- [クォータニオン (Quaternion) を総整理！ ～ 三次元物体の回転と姿勢を鮮やかに扱う ～](https://qiita.com/drken/items/0639cf34cce14e8d58a5)