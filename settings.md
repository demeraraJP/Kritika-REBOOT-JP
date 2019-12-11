# はじめに

ゲームが重たい時の対処法です。  
特に低スペックの PC やノート PC などに有効です。  
頻繁にクラッシュするような方も一度目を通してみてください。

ゲーム外設定では、文字サイズの変更方法やキー設定の方法などについても触れています。

ゲームフォルダは Steam のライブラリで、  
KritikaREBOOT を右クリック -> 管理 -> ローカルファイルを閲覧  
で、一発で開けます。

注意：オプションファイルを編集する行為は、一度読んですぐに理解できる人だけ行ってください。よくわからないのに下手にいじるとゲームファイルを破損させてしまい再インストールするはめになるかもしれません。



# 目次

- ゲーム内設定

  1.[ラグを改善する最も簡単で効果的な方法](#1ラグを改善する最も簡単で効果的な方法)  
  2.[パーティメンバーのエフェクトを消す、または減らす](#2パーティメンバーのエフェクトを消す、または減らす)  
  3.[ダメージ表示の簡略化](#3ダメージ表示の簡略化)  
  4.[備考](#4備考)

- ゲーム外設定(オプションファイルの編集)

  1.[フリーズやクラッシュを改善](#1フリーズやクラッシュを改善)  
  2.[解像度の設定が毎回リセットされてしまう問題](#2解像度の設定が毎回リセットされてしまう問題)  
  3.[文字が小さくて読めない場合](#3文字が小さくて読めない場合)  
  4.[アイテムを自動で拾う](#4アイテムを自動で拾う)  
  5.[一度のクリックで二回分クリックしたことにする](#5一度のクリックで二回分クリックしたことにする)



# ゲーム内設定

## 1.ラグを改善する最も簡単で効果的な方法

まずは ESC を押して設定画面を開きます。

`ESC -> System Settings -> Graphics`

最初に一番上の項目の **Resolution** の数字が自身の使っている PC のモニターと同じ解像度になっているか確認します。デフォルトで同じ解像度になっていると思うのでよくわらない人はそのままでいいです。  
次にその隣の **Screen Mode** をフルスクリーンにします。ウィンドウモードは GPU の負荷が高くなるのでやめてください。

その 2 つを確認したら、少し下の _Advanced Settings_ にある **Lightmap Quality** の項目
を[None]にします。

PC によってはこれだけで大幅にラグが改善します。とりあえずこれだけ設定して暫く様子を見てください。


## 2.パーティメンバーのエフェクトを消す、または減らす

ソロだと問題ないけど、パーティだと重たいんだよねという人向け  
上記と同じ _Advanced Settings_ の一番下に、 **Show other charcter** という項目があるので、これを[OFF]にします。  
これを[OFF]にしても他のキャラクターは表示されます。パーティメンバーのエフェクトを表示しないという設定です。  
パーティメンバーのボイスも聞こえなくなるので若干寂しいです…。

加えて、_Advanced Settings_ の上にある、 **Party Transparentness** という項目のスライダーを左にずらします。  
ずらした分だけエフェクト量が減るので軽くなります。  
上記の項目とは別の部分のエフェクトなので、それぞれ設定しましょう。


## 3.ダメージ表示の簡略化

`ESC -> System Settings -> UI Configuration`(一番最後のタブ)

このタブにある **Show damage** という項目を[Simplify]に設定します。  
モンスターに与えたダメージの表記が 537K とか 19M という表示方法に変わります。

画面に表示される文字数が大幅に減るため、視界が開けるという意味でも助かります。


## 4.備考

これでも重たい人は Advanced Settings にある他の項目もできる限り、[None]か[OFF]、または[Close]にしましょう。  
ただし、 **Texture Size** と **My character effects** 及び **Special Texture Quality** はいじらない方が無難です。場合によっては表示が崩れたり、まともにゲームがプレイできなくなったりします。

あと、まれに **Vertical sync** (垂直同期)が[ON]になっている場合があるので、ラグを感じるようなら必ず[OFF]にしましょう。



# ゲーム外設定(オプションファイルの編集)

## 1.フリーズやクラッシュを改善

特にレイドで、落ちたり固まったりするという人は以下に記す方法を試してみてください。

編集するファイルはデフォルト設定の場合次の場所にあります  
"C:\Program Files (x86)\Steam\steamapps\common\Kritika\resource\applemain"

この applemain のフォルダの中から以下の 3 つのファイルを探します。

- DefaultHigh.xml
- DefaultLow.xml
- DefaultMedium.xml

これらのファイルを右クリックして、[メモ帳で開く]を選択。表示されない場合は、[その他のプログラムで開く]から[メモ帳]を探して選択してください。  
開いたら次の一行を探し、 **100** という数字を **60** に書き換えます。

`<ForegroundMaxFrameRate type="float" value="100"/>`

これを、

`<ForegroundMaxFrameRate type="float" value="60"/>`

とします。

書き換えたら上書き保存(Ctrl+S)してメモ帳を終了してください。

この変更を 3 つ全てのファイルに行います。

※FPS値の上限を上げたい場合は、この数値を 150 や 240 等、任意の数字に書き換えてください。ただし、レイドで落ちる確率が増す可能性があります。


## 2.解像度の設定が毎回リセットされてしまう問題

ゲームを起動するたびに、設定したはずの解像度がリセットされてしまう問題の解決方法です。  
これを試してもダメな人もいるようですが、一応参考程度に載せておきます。

場所："C:\Program Files (x86)\Steam\steamapps\common\Kritika"

Kritika の exe ファイルが入ってるフォルダです。[はじめに](#はじめに)の方法で簡単に開くことができます。
そこに **option.xml** というファイルがあると思うので探して見てください。

このファイルではゲーム内の様々な設定ができます。  
上記同様、このファイルも右クリックからメモ帳で開きます。

17 行目に

`<Resolution type="int2" value="(1280, 720 )" />`

という一文があると思います。見当たらない場合はこれをこのままコピペして、以下の場所に追加してください。(<\/Audio> と <FXAAenable ~> の間)

```xml
    </volume>
</Audio>
<Resolution type="int2" value="(1280, 720 )" />
<FXAAEnable type="uint32" value="0" />
<TextureSize type="uint32" value="0" />
```

この`value="(1280, 720 )"`の数値を、自身が使用しているモニターと同じ解像度に設定します。

たとえば

`<Resolution type="int2" value="(1366, 768 )" />`

といった風に。

書き換えたら上書き保存(Ctrl+S)してメモ帳を閉じてください。


## 3.文字が小さくて読めない場合

英語フォントは日本語フォントに比べてどうしても文字が小さく見えます。  
小さくて読めないという人は、ゲームフォルダの中にあるテキストファイルをメモ帳等で開いてフォントサイズを書き換えることで、文字の大きさを変えることができます。

場所："C:\Program Files (x86)\Steam\steamapps\common\Kritika\resource\Common\database"  
この場所にある **FontConfig_en-EN.txt** というテキストファイルを右クリックして、[メモ帳で開く]を選択。表示されない場合は、[その他のプログラムで開く]から[メモ帳]を探してください。

※PCのスペックが低い場合、データが若干大きいためにメモ帳がフリーズしたりクラッシュして開けないことがあります。その場合は、「notepad++」や「サクラエディタ」等の無料で軽量のテキストエディタをインストールして使ってみてください。ちょっと調べれば使い方はすぐにわかります。

さて、メモ帳やテキストエディタ等で **FontConfig_en-EN.txt** を開いたら、上から 3 行目にある

`map "$NormalFont" = "Ubuntu Condensed" Normal 1`

という項目の最後の数字を書き換えます。  
1 が標準の大きさで、1.1 にすると 10%大きくなります。1.1~1.5 くらいまでの好きな数字に書き換えてください。おすすめは 1.2 です。1.3 以上になると文字がはみ出すようになります。

それで、

`map "$NormalFont" = "Ubuntu Condensed" Normal 1.2`

という風に書き換えられたらファイルを上書き保存(Ctrl+S)してファイルを閉じてください。

注意：数字は必ず半角で入力してください。全角だと認識してくれません。


## 4.アイテムを自動で拾う

ペットがいるから関係ないや  
と思うかもしれませんが、ペットがいても F キーを押すと素早くアイテムが拾えるのです。  
その F キーを前進キー(W)に割り当てて一度でも前進するとアイテム自動拾得機能をオンにし、指を離しても自動的に素早くアイテムが拾えるようにするテクニックです。  
若干内容が高度かもしれません。

まずは、[はじめに](#はじめに)の方法でゲームフォルダを開きましょう。  
フォルダ内にある **option.xml** をコピー(Ctrl+C)して同じ場所に複製(Ctrl+V)します。

- option.xml
- option\_コピー.xml

次に、ファイル名の"コピー"の部分を効果を適用させたい自身のキャラクター名に書き換えます。  
ファイル名は、`option[半角アンダーバー][キャラクター名].xml` となります。

- option.xml
- option_Demerara.xml

書き換え終わったら、そのリネームしたファイルを右クリックしてメモ帳で開きます。

ファイルが開いたら、検索機能(Ctrl+F)で"pick"を検索します。

すると次のブロックが見つかると思います。

```xml
<item type="Apple::InputCommandItem">
    <key type="wstring" value="F" />
    <name type="wstring" value="InGamePage.BeginPickUpItem" />
    <state type="wstring" value="press" />
    <activeState type="wstring" value="" />
    <withKey type="wstring" value="" />
</item>
<item type="Apple::InputCommandItem">
    <key type="wstring" value="F" />
    <name type="wstring" value="InGamePage.EndPickUpItem" />
    <state type="wstring" value="release" />
    <activeState type="wstring" value="" />
    <withKey type="wstring" value="" />
</item>
```

上のブロックは、F キーを押している間(press)、アイテムを拾う(InGamePage.BeginPickUpItem)というコードで、下のブロックは、F キーを離した(release)とき、アイテムを拾うことをやめる(InGamePage.EndPickUpItem)というコードです。

この上のブロックの`<key type="wstring" value="F" />`の F を W に書き換えます。

そして下のブロックにもある同じ`<key type="wstring" value="F" />`の F を F4 にします。

```xml
<item type="Apple::InputCommandItem">
    <key type="wstring" value="W" />
    <name type="wstring" value="InGamePage.BeginPickUpItem" />
    <state type="wstring" value="press" />
    <activeState type="wstring" value="" />
    <withKey type="wstring" value="" />
</item>
<item type="Apple::InputCommandItem">
    <key type="wstring" value="F4" />
    <name type="wstring" value="InGamePage.EndPickUpItem" />
    <state type="wstring" value="release" />
    <activeState type="wstring" value="" />
    <withKey type="wstring" value="" />
</item>
```

これで前進キー(W)を一度でも押すと、ずっと W を押し続けている状態になり自動でアイテムを拾うようになります。  
そして、この状態を解除するためのキーを F4 に設定しました。つまり、リスタートするたびにこの自動拾得機能を解除します。  
こうしないとリスタート直後にアイテムを拾うコマンドが動き続けるために、"can't pick up items"(アイテムを拾えません)というエラーログが大量に流れることになります。

これはあくまで一つの例です。自分好みのキーに設定してみてください。

ファイルを上書き保存(Ctrl+S)してメモ帳を閉じたら完成です。

全てのキャラクターに適用させるためには、完成したファイルをコピペでキャラクターの数だけ増やして、それぞれのキャラクター名にリネームするだけです。

※キャラクターの Lv が 15 以上じゃないと適用されないらしいです。あと、大型のアプデとかあると初期化されることがあります。バックアップ取っておくと吉。


## 5.一度のクリックで二回分クリックしたことにする

影術師でクライゼンシュラークを早打ちするために使われる(使われた)テクニックです。

※手動で連打する場合に限り有効です。Auto-Attack では発動しません。

4.[アイテムを自動で拾う](#4アイテムを自動で拾う)で作ったキャラクター毎のオプションファイルを開きます。作ってない方は、このトピックを読んで作成してください。

今度は"and no"と検索します。

すると、ヒット数 3 件で次のブロックが表示されるはずです。

```xml
<item type="Apple::InputCommandItem">
    <key type="wstring" value="LeftMouse" />
    <name type="wstring" value="InGamePage.ActionCommand NormalAtk" />
    <state type="wstring" value="down" />
    <activeState type="wstring" value="" />
    <withKey type="wstring" value="" />
</item>
<item type="Apple::InputCommandItem">
    <key type="wstring" value="LeftMouse" />
    <name type="wstring" value="InGamePage.ActionCommand NormalAtk" />
    <state type="wstring" value="DoubleClick" />
    <activeState type="wstring" value="" />
    <withKey type="wstring" value="" />
</item>
<item type="Apple::InputCommandItem">
    <key type="wstring" value="LeftMouse" />
    <name type="wstring" value="InGamePage.ActionCommand NormalAtk_up" />
    <state type="wstring" value="up" />
    <activeState type="wstring" value="" />
    <withKey type="wstring" value="" />
</item>
```

このブロックの下に次のブロックを追加します。

```xml
<item type="Apple::InputCommandItem">
    <key type="wstring" value="LeftMouse" />
    <name type="wstring" value="InGamePage.ActionCommand NormalAtk" />
    <state type="wstring" value="up" />
    <activeState type="wstring" value="" />
    <withKey type="wstring" value="" />
</item>
<item type="Apple::InputCommandItem">
    <key type="wstring" value="LeftMouse" />
    <name type="wstring" value="InGamePage.ActionCommand NormalAtk" />
    <state type="wstring" value="DoubleClick" />
    <activeState type="wstring" value="" />
    <withKey type="wstring" value="" />
</item>
<item type="Apple::InputCommandItem">
    <key type="wstring" value="LeftMouse" />
    <name type="wstring" value="InGamePage.ActionCommand NormalAtk_up" />
    <state type="wstring" value="up" />
    <activeState type="wstring" value="" />
    <withKey type="wstring" value="" />
</item>
```

これだけです。
あとは上書き保存(Ctrl+S)してメモ帳を閉じれば完成です。

このブロックを追加することで、マウスの左クリックを一回押した際(厳密に言うと離した際)、二度攻撃を行うようになり、**手動で連打する場合に限り**クライゼンシュラークを素早く打てるようになります。

ただ、残念ながら(?) Guns 刻印が改編されたことにより、クライゼンシュラークの発射回数が減って Auto-Attack でも十分素早く打てるようになってしまいました。この裏技が使われることはもうないかもしれません…。
