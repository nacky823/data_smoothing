# データ平滑化プログラム
連続したアドレスに保存されているデータを、
平滑化して同じアドレスに上書き保存するプログラムです。

## インストール
```
git clone https://github.com/nacky823/data_smoothing.git
```

## プログラムの説明

例えば、100個の連続のアドレスに保存された、

`float`型のデータ $x$ $(x_0, x_1, ..., x_{99})$ があり、
整数 $a = 2$ とする。

任意のデータを $x_i$ $(0 \leq i \leq 99)$ と表し、

$x_i$ より順番が前のデータ $a$ 個と、

$x_i$ より順番が後のデータ $a$ 個と、

$x_i$ の合計を計算し、それを母数である $a + a + 1 = 5$ で割る。

その結果を $y_i$ とすると、$y_i = (x_{i-2} + x_{i-1} + x_i + x_{i+1} + x_{i+2}) / 5$ となる。

この $y_i$ を $x_i$ と同じアドレスに保存する。

あとはこれを $i = 0$ から $i = 99$ の範囲全てで行う。

## 使用方法
1. （任意）main.c を編集
    + 3, 4 行目を編集
    ```c
    #define DATA_SIZE 20
    #define ADJACENT  3
    ```
    > `DATA_SIZE` は動作確認のために作成する、連続するデータの個数  
    > `ADJACENT` は前後何個分を母数として使用するか（母数が 5 なら 2）
1. このリポジトリのディレクトリに移動
    ```
    cd data_smoothing/
    ```
1. コンパイル
    ```
    make
    ```
1. 以下のコマンドを実行
    ```
    ./run
    ```
1. 実行結果の確認
    ```
    Data initialization
    
    data[0] = 0.000000
    data[1] = 0.000000
    data[2] = 0.000000
    data[3] = 1.000000
    data[4] = 1.000000
    data[5] = 1.000000
    data[6] = 2.000000
    data[7] = 2.000000
    data[8] = 2.000000
    data[9] = 3.000000
    data[10] = 3.000000
    data[11] = 3.000000
    data[12] = 4.000000
    data[13] = 4.000000
    data[14] = 4.000000
    data[15] = 5.000000
    data[16] = 5.000000
    data[17] = 5.000000
    data[18] = 6.000000
    data[19] = 6.000000
    
    Data smoothing
    
    data[0] = 0.000000
    data[1] = 0.000000
    data[2] = 0.000000
    data[3] = 0.714286
    data[4] = 1.000000
    data[5] = 1.285714
    data[6] = 1.714286
    data[7] = 2.000000
    data[8] = 2.285714
    data[9] = 2.714286
    data[10] = 3.000000
    data[11] = 3.285714
    data[12] = 3.714286
    data[13] = 4.000000
    data[14] = 4.285714
    data[15] = 4.714286
    data[16] = 5.000000
    data[17] = 5.000000
    data[18] = 6.000000
    data[19] = 6.000000
    ```

    > 正常に動作すると上記のような出力結果が得られる。  
    > `Data initialization` に続く出力が、平滑化前のデータ。  
    > `Data smoothing` に続く出力が、平滑後のデータ。

### 組込み実装で使用する場合
1. インクルードファイルディレクトリに `smoothing.h` をコピー
1. ソースファイルディレクトリに `smoothing.c` をコピー
1. 適切な形式でコンパイル

## ライセンス

このソフトウェアパッケージは、Apache License 2.0 のもと、再配布および使用が許可されます。

© 2023 nacky823