# 演習1（構造）
## 1. 演習課題
以下のような単純梁をGrasshopper + Karamba3Dで解析します。

![](img/2022-05-05-21-15-20.png)

鋼材のヤング係数E=205000N/mm<sup>2</sup>

断面 H - 400 x 200 x 8 x 13 ( Ix=22965cm<sup>4</sup> Zx = 1148cm<sup>3</sup>)

点BはACの中点とする。

## 2. Grasshopperによる描画


grasshopper上で節点及び線を描画します。

点A　原点（ 0, 0, 0 )

点B　AC間の中心（ L / 2, 0, 0 )

点C　　　（ L, 0, 0 )

スパンLはNumberSliderでパラメーターとして設定します。

![](img/2022-04-28-11-25-25.png)

### 2.1 コンポーネントの配置例1

コンポーネントのみで配置した例

![](img/2022-04-27-20-18-24.png)

使用コンポーネント

・Panel

・Division(Maths → Opeators)

・Number Slider(Params → Input)

・Construction Point(Vector → Point)

・Line(Curve → Primitive)

### 2.2 コンポーネントの配置例2

ghPythonを使用した例

![](img/2022-05-05-21-20-07.png)

ghPythonではジオメトリを格納した変数をコンポーネントの出力変数名に一致させる必要があります。

```python
import rhinoscriptsyntax as rs

# 座標の定義（タプルで定義します。リストでも可）
crdA = (  0,0,0)
crdB = (L/2,0,0)
crdC = (  L,0,0)

# 節点の定義
ptA = rs.AddPoint(crdA) 
ptB = rs.AddPoint(crdB)
ptC = rs.AddPoint(crdC)

# 要素（LINE）の定義
elemAB = rs.AddLine( crdA, crdB )
elemBC = rs.AddLine( crdB, crdC )

```

## 3. Karamba3Dによる解析


1.支点（境界条件）の定義

2.要素の定義

3.材料の定義（鉄骨）

4.断面形状の定義（H形鋼）

5.分布荷重の設定

6.解析モデルの構築

7.解析

8.出力（モデル及び梁要素）

![](img/2022-04-29-23-45-09.png)

使用コンポーネント

・Support(Karamba3D → Model)

・LineToBeam(Karamba3D → Model)

・MaterialSection(Karamba3D → Materials)

・CrossSection(Karamba3D → Cross Section)

・Loads(Karamba3D → Load)

・Assemble(Karamba3D → Algorithms)

・Analyze(Karamba3D → Algorithms)

・Model View(Karamba3D → Results)

・Beam View(Karamba3D → Results)

## 4.検証

解析結果が出たら中央の曲げモーメント及び中央（B点）の変形量について検証を行います。

単純梁の最大（中央部）の曲げモーメント

<img src="https://latex.codecogs.com/svg.image?M=\frac{1}{8}&space;wL^{2}">

中央部の変形

<img src="https://latex.codecogs.com/svg.image?\delta=\frac{5wL^{4}}{384EI}&space;">

ここに

スパン：L、分布荷重：w、ヤング係数：E、断面二次モーメント：I

各自、手計算（電卓・Excelなど）で検証してみましょう。

※ 手計算ではせん断変形の影響を無視していますので、変形は若干小さめになります。
