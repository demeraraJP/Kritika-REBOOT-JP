# はじめに

ここではオプションファイルの編集方法を紹介します。  
オプションファイルは、ゲーム内では設定できないようなことまで設定できるので編集方法を知っていると何かと便利です。

※PCが不慣れな人にとっては若干高度な内容になるかもしれません。何度読んでもわからないような場合は、触らない方が賢明です。  
※万が一この方法を利用したことにより何かしらの損害が発生したとしてもdemeraraJPは一切責任を負いません。全て自己責任でお願いします。  
※この方法は韓国でサービスが開始された当初から利用されているもので、運営も公式の掲示板で認めた合法な手段です。自身も日本サービスの際に運営に直接確認しましたが、オプションファイルの編集は問題ないとの返答を頂いています。スクリプトを書き換えたり、ショップポイントを不正に得るようなチートやハッキングの類ではありません。あくまでオプションの変更が目的です。それでも気になるような方は読まないでください。


## テキストエディタの導入

以下に記す編集方法は基本的にメモ帳でも出来ますが、テキストエディタがあると作業がスムーズに行なえます。  
テキストエディタは簡単に言うと高機能な文章編集ソフトです。プログラマーなんかがコードを書いたりするのに使うイメージですが、文章を編集する際にもとても便利なのでよかったら使ってみてください。  
「notepad++」や「サクラエディタ」が軽量な上に無料で使えるのでおすすめです。

とりあえずメモ帳でやってみて、大変だなと思ったら調べてみるといいかもしれません。

## ゲームフォルダを開く

ゲームフォルダは Steam のライブラリで、左に並んでるタイトルのKritikaREBOOT を右クリック -> [管理] -> [ローカルファイルを閲覧] で、一発で開けます。


# 目次

1.[文字のサイズを大きくする](#1文字のサイズを大きくする)  
2.[アイテムを自動で拾う](#2アイテムを自動で拾う)  
3.[一度のクリックで二回分クリックしたことにする](#3一度のクリックで二回分クリックしたことにする)  
4.[無限通常攻撃](#4無限通常攻撃)


## 1.文字のサイズを大きくする

英語フォントは日本語フォントに比べてどうしても文字が小さく見えます。  
小さくて読めないという人は、ゲームフォルダの中にあるテキストファイルをメモ帳等で開いてフォントサイズを書き換えることで、文字の大きさを変えることができます。

先ずはゲームフォルダを開きます。
`resource -> Common -> database` と順に開いていきます。(パス"C:\Program Files (x86)\Steam\steamapps\common\Kritika\resource\Common\database")

_database_ フォルダの中にある **FontConfig_en-EN.txt** というテキストファイルを右クリックして、[メモ帳で開く]を選択。表示されない場合は、[その他のプログラムで開く]から[メモ帳]を探してください。

※PCのスペックが低い場合、データが若干大きいためにメモ帳がフリーズしたりクラッシュして開けないことがあります。その場合は、[テキストエディタの導入](#テキストエディタの導入)を検討してみてください。

さて、メモ帳やテキストエディタ等で **FontConfig_en-EN.txt** を開いたら、上から 3 行目にある

`map "$NormalFont" = "Ubuntu Condensed" Normal 1`

という項目の最後の数字を書き換えます。  
1 が標準の大きさで、1.1 にすると 10%大きくなります。1.1~1.5 くらいまでの好きな数字に書き換えてください。おすすめは 1.2 です。1.3 以上になると文字がはみ出すようになります。

それで、

`map "$NormalFont" = "Ubuntu Condensed" Normal 1.2`

という風に書き換えられたらファイルを上書き保存(Ctrl+S)してファイルを閉じてください。

注意：数字は必ず半角で入力してください。全角だと認識してくれません。


## 2.アイテムを自動で拾う

ペットがいるから関係ないや  
と思うかもしれませんが、ペットがいても F キーを押すと素早くアイテムが拾えるのです。  
その F キーを前進キー(W)に割り当てて一度でも前進するとアイテム自動拾得機能をオンにし、指を離しても自動的に素早くアイテムが拾えるようにするテクニックです。

先ずはゲームフォルダを開きます。

次にその場所にある **option.xml** をコピー(Ctrl+C)して同じ場所に複製(Ctrl+V)します。

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
こうしないとリスタート直後にアイテムを拾うコマンドが動き続けるために、"Cannot pick up items."(アイテムを拾えません)というエラーログが大量に流れることになります。

と、思ったんですがこれだとポータル移動で別のステージ入った場合、エラーログが流れてしまうので自分はアイテム修理の F1 に設定しました。

ここまではよかったんですが、問題は死んでしまったときです。KRITIKAでは何故か死んだ時も入力を受け付け、それが実行できないためにエラーログが流れます。復活待機時間があるとその間ずーっと流れ続けます。"Unable to find player to pick up items" や "Cannot recieve items when dead" のように、死んだ状態ではアイテムを受け取れないという旨のメッセージが永遠に流れてしまいます。

これを止めるには、先程設定した F1 を押せばいいのですが、いちいち押すのも面倒くさいので自分はエラーメッセージ自体を消してしまいました。ただし、この方法は KRITIKA 自体のコンテンツを削除する行為にあたるため、かなりグレーだと思ってます。なのでここではその方法のヒントだけ書くことにします。

※ヒント：[文字のサイズを大きくする](#1文字のサイズを大きくする)で使用したファイルは、韓国語を英語に翻訳したテキストファイルです。ここに書かれている文章がゲーム中に表示されるようになっています。コードは全て一緒で、`tr "(スクリプト)" = "(ゲーム中に表示される文章)"` となっています。このコード自体を消してしまうと、スクリプトが直接表示されてしまうのでいただけないです。

ファイルを上書き保存(Ctrl+S)してメモ帳を閉じたら完成です。

全てのキャラクターに適用させるためには、完成したファイルをコピペでキャラクターの数だけ増やして、それぞれのキャラクター名にリネームするだけです。

※キャラクターの Lv が 15 以上じゃないと適用されないらしいです。

## 3.一度のクリックで二回分クリックしたことにする

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


## 4.無限通常攻撃

もうここまでくるとバグ技みたいなもんですが、こういう色んなことがオプションファイルで設定できてしまうというのもKRITIKAの面白さかもしれません。最近のゲームがほとんどレジストリで管理するようになってるので、こんな風に自由には設定できなかったりします。

では、早速その方法の紹介です。今回は至って簡単です。
[一度のクリックで二回分クリックしたことにする](#3一度のクリックで二回分クリックしたことにする)で利用した"NormalAtk"のコードを検索します。

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

このブロックの3つ目だけ、3行目の最後が `NormalAtk_up` になっているのがわかると思います。  
この最後の `_up` を消します。以上です。

注意：[一度のクリックで二回分クリックしたことにする](#3一度のクリックで二回分クリックしたことにする)で変更を加えたキャラクターでは設定しないでください。多重クリックが発生してしまいます。どちらか一方の方法だけ使用するようにしてください。

これを設定した状態でステージに入場し、一度でも左クリックを押すと永遠に通常攻撃をし続けます。特定のスキルで入力をキャンセルするかステージをクリアするまで止まりません。狂戦士のマッドラッシュとかめちゃくちゃ速くなりますが、まあ不便ですよね。うん。
