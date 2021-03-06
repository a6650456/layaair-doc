# F9！项目设置介绍

>本編ではLayaAirIDE 2.0.1 bateスクリーンショットを採用していますが、異なる場合は最新のLayaAirIDEをダウンロードして最新バージョンIDEに準じてください。

##概要

ショートカットキーF 9はLayaIDEが一番よく使われています。最も不可欠な機能です。Layaを熟知している開発者はF 9の重要性を知っています。この点は早くも1.0で開発者たちに知られています。2.0エンジンでF 9を使わないといけないです。しかし、Layaに接触したばかりの開発者がF 9の機能を知らないので、この記事では紹介します。（熟練者は本編を無視してもいいです。）





###一、プレビューの設定

項目設定の最初のページはプレビュー設定で、ここでは主に開始シーン（プログラム起動時に最初にロードされたシーン、現在のシーンを選択するとエディタの最後の焦点があるシーン）と他の設定があります。この設定はIDEの自動生成タイプGameConfigに影響します。手動でこのクラスを変更すると無効になります。IDEでしか設定できません。

！[](img/1.png)



GameConfigは以下の図の通りです。

！[](img/7 png)

対応する現在のシーンコードを起動します。Mainクラスでは、開発者が自分のニーズに応じてデフォルトの起動設定を使用しなくてもいいです。！[](img/8 png)



###二、クラス設定

コードパッケージのサイズを小さくするために、開発者は使用したクラスライブラリだけを導入してもいいです。使用していない機能はコードパッケージのサイズを使わなくてもいいです。

ライブラリ設定は非常に一般的な機能であり、Webglライブラリにチェックを付ける場合、エンジン初期化はwebglモード、逆にcanvasモードとなります。

他のクラスは実際の需要に応じて自分で取捨選択することができます。ライブラリをチェックしていないのに、ライブラリ機能を使うとエラーが発生します。



！[](img/2 png)



###三、シーン設定

ここでは一般的に動く必要がありません。主にリリースモードです。ミニゲームのコードパッケージサイズを減らすために、IDEはデフォルトではファイルモードです。

四つのパターンの違いは以下の通りです。


 **埋め込みモード**埋め込みモードでは、エディタのUIコンテンツをシーンコードファイルに生成します。コードスクリプトにはIDEで作成されたUIシーンの情報が含まれています。ミニゲームやライトゲームがまだ登場していない時は、jsのサイズを考慮しないで、正常にh 5を開発するのに一番よく使われる選択です。

**読み込みモード**ロードモードもシーンタイプを生成します。他のUIデータ情報は1つのui.jsonに入れられます。使う時はこのJsonをロードしなければなりません。同じように、小さいゲームがない時代にはあまり使われません。シーン情報はjsになくてもいいです。jsパッケージのサイズを節約して、ゲーム4 mにもっと多くのスペースを節約できます。リソースとして使用できます。

**分離モード**分離モードはロードモードに基づいて、シーンクラスも同様に生成されるが、彼はシーンごとに個別のシーンデータファイルを生成し、シーンファイルを個別にロードするたびに、ロードモードとは違って、一度にすべてのシーンをロードする。2.0以降は、ミニゲームやライトゲームを開発し、メインパックの大きさを減らすためにも、ロード速度を上げるためにも一般的なモデルです。

**ファイルモード**ファイルモードは2.0特有で、ミニゲームを開発するために作成されたものです。彼はシーンクラスを生成しないで、jsパッケージのサイズをさらに減らすことができます。使う時はScene.load方式でロードします。前の3つの最大の違いは、ファイルモードが直接シーン内の変数を呼び出すことができないので、getwindを取得してから操作する必要があります。前の3つのシーンクラスは変数を宣言しています。コードヒントがあります。直接内部の変数を操作できます。



#####注意したいのは、js言語の開発を選ぶ時、分離モードとファイルモードは区別がなくて、シーン種類がありません。



！[](img/3 png)



###四、図集の設定

図集の設定は自動的に図集を包装する各規則を設定できます。カタログは変更しないほうがいいです。

！[](img/4 png)



###五、設定を編集する

図のように、これはあまり紹介しません。

！[](img/5 png)