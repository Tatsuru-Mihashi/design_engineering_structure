# 演習1（構造）
## 単純梁の解析
以下のような単純梁をGrasshopper + Karamba3Dで解析します。

![](img/2022-04-27-20-32-10.png)

## Grasshopperによる描画


grasshopper上で節点及び線を描画します。

点A　原点（ 0, 0, 0 )

点B　AC間の中心（ L / 2, 0, 0 )

点C　　　（ L, 0, 0 )

スパンLはNumberSliderでパラメーターとして設定します。

![](img/2022-04-28-11-25-25.png)

## コンポーネントの配置例

以下にコンポーネントの配置例を示します。他にも様々な方法があります。

![](img/2022-04-27-20-18-24.png)

使用コンポーネント

・Panel

・Division(Maths → Opeators)

・Number Slider(Params → Input)

・Construction Point(Vector → Point)

・Line(Curve → Primitive)


## Karamba3Dによる解析


1.支点（境界条件）の設定

2.梁要素の設定

3.断面形状の定義（H形鋼）

4.材料の定義（鉄骨）

5.分布荷重の設定

6.解析モデルの構築

7.解析

8.出力（モデル及び梁要素）

![](img/2022-04-27-20-52-56.png)

使用コンポーネント

・Support(Karamba3D → Model)

・LineToBeam(Karamba3D → Model)

・Cross Section(Karamba3D → Cross Section)

・Materials(Karamba3D → Materials)

・Loads(Karamba3D → Load)

・Assemble(Karamba3D → Algorithms)

・Analyze(Karamba3D → Algorithms)

・Model View(Karamba3D → Results)

・Beam View(Karamba3D → Results)

## 検証

解析結果が出たら中央の曲げモーメント及び中央（B点）の変形量について検証を行います。
検証に使う断面二次モーメントはIx=cm4 とします。

単純梁の中央の曲げモーメント

<img src="https://latex.codecogs.com/svg.image?M=\frac{1}{8}&space;wL^{2}">

中央部の変形

<img src="https://latex.codecogs.com/svg.image?\delta=\frac{5wL^{4}}{384EI}&space;">

ここに
スパン：    L
分布荷重：  w
ヤング係数：E
断面二次モーメント：I


