# My solution of Three
`three` というバイナリが与えられている．

ひとまず`strings`コマンドを試してみるが，FLAGは見つからない．

という訳で，Ghidraさんに頼る．

main関数の内容をDecompilerで眺めると，`validate_flag`といういかにも怪しげな関数が見つかる．

<figure><img src="../assets/solve1.png" alt=""></figure>

関数`validate_flag`を眺める．

どうやら，`local_c`を3で割った余りが0の時は変数`flag_0`，余りが1の時は変数`flag_1`，余りが2の時は変数`flag_2`から値を取り出している模様．

<figure><img src="../assets/solve2.png" alt=""></figure>

これは変数`flag_0`，`flag_1`，`flag_2`にFLAG文字列が格納されていると踏んで，値をchar型に設定することに．

変数を選択し，「Retype Global」を選んで，型としてcharを入力．
<figure><img src="../assets/solve3.png" alt=""></figure>
<figure><img src="../assets/solve4.png" alt=""></figure>

変数`flag_0`は`c`を先頭文字列として格納する配列だと判明．

おそらく`ctf4b{......}`の`c`だと推測．

<figure><img src="../assets/solve5.png" alt=""></figure>

変数`flag_1`，`flag_2`についても同様に型をcharに変更．

<figure><img src="../assets/solve6.png" alt=""></figure>

`c`，`t`，`f`の文字が見える．

各変数の中身を見ていくと，内容もFLAGらしい文字列（`{` `}`とか`_`とかが含まれている）になっている．

<figure><img src="../assets/solve7.png" alt=""></figure>
<figure><img src="../assets/solve8.png" alt=""></figure>
<figure><img src="../assets/solve9.png" alt=""></figure>

後は，`local_c`を3で割った余りが0の時は変数`flag_0`，余りが1の時は変数`flag_1`，余りが2の時は変数`flag_2`から値を取り出していたことを踏まえて，文字列を連結．
```
flag_0 = c4c_ub__dt_r_1_4}
flag_1 = tb4y_1tu04tesifg
flag_2 = f{n0ae0n_e4ept13
```

左上から順に縦に読んでいけばOK．

```
ctf4b{c4n_y0u_ab1e_t0_und0_t4e_t4ree_sp1it_f14g3}
```

# 補足
なお，このような暗号をスキュタレー暗号と呼ぶ．
