#LayaAir機能紹介

>LayaAirエンジンは主にエンジンライブラリとLayaAir IDEの二つのコア部分を含んでいます。
>
>LayaCloudとLayaNativeはエンジンの生態系の部分です。



##LayaAir 2.0エンジンライブラリ機能

LayaAir 2.0エンジンは1.0の既存機能を維持しているだけでなく、例えば：

精霊、ベクトル図、テキスト、リッチテキスト、ビットマップフォント、アニメーション、骨格、オーディオとビデオ、フィルタ、イベント、ローディング、緩動、時間、ネットワーク、UIシステム、物理システム、TiledMap、prtocolなどのAPI。

さらに、box 2 dの物理エンジン、コンポーネント化サポート、および150以上の3 D機能を内蔵しています。

新たに追加された主な公式素材はPBRSTANDARD Material、PBRSpecular Material、Unilit Materialなどがあります。

テクスチャについては、テクスチャパラメータ構成（mipmap、format、wrapModeU、wrapModeV、filterMode、anisoLevel）を追加し、テクスチャアップロード画素インターフェースを追加し、GPUテクスチャ圧縮を行う。

アニメの面では、アニメイトのアニメ融合機能のcrossFadeを追加し、アニメのマルチメディアミックス放送を追加し、アニメの更新メカニズムをリアルタイム補間に調整し、メモリとアニメの流暢さの表現を大幅に減少させ、様々な材質の属性のアニメを追加しました。

2 D、3 D、VRの開発をサポートして、CanvasとWebGLモードをサポートして、同時にHTML 5、Flash、APP（IOS、Android）の微信小ゲームとして発表して、QQは多種のバージョンを遊びます。


##LayaAir 2.0 IDE機能

LayaAir 2.0 IDEは主に含まれています。`项目管理`を選択します`代码开发编辑器`を選択します`可视化编辑器`を選択します`第三方工具链支持工具`など。

主な機能は以下を含む。

##-コード開発UIとシーンエディタ
##-シーン管理（2.0追加）粒子エディタ
##-アニメーションエディタ物理エディタ(2.0追加)
##-コンポーネント化サポート（2.0追加）3 D対応（2.0追加）
##-LayaCloudプロジェクトサポート（2.0追加）スクリプト拡張
##-プリセットAPPパッケージ
##-JS混淆と圧縮第三者ツールチェーン変換ツール（Unity 3 D、TiledMap、Spine、竜骨…）



Laya 2.0 IDE互換LayaAir 1.xバージョンの書き方は、2 dプロジェクトの中で、あまり大きな変更がなくても大丈夫です。元のプロジェクトを2.0エンジンにアップグレードできます。

Laya 2.0 IDEはマウントコンポーネントスクリプトとシーン管理の方式で開発し、ideでシーンとページコンポーネントを編集し、シナリオを追加することによって、プロジェクト開発がプログラム、美術、企画の共同作業に有利になり、Layaに初めて接触した開発者に対して、より使いやすく、より友好的な開発方式になります。



##LayaNative機能

LayaNativeはLayaAirエンジンのモバイル端末向けアプリの開発、テスト、リリースの完全な開発ソリューションですが、LayaAirエンジンに限られません。LayaNativeはLayaPlayerを中心に運行している時に、反射機構、チャンネルドッキングプログラムを利用して開発者が元のAppで二次オープンとチャンネルドッキングを行い、テスター、構築ツールを提供して、開発者のためにhtml 5プロジェクトを包装し、元のApに発表して便利です。

####LayaNative 2.0はコード再構成を経て、性能は1.0バージョンと比較して大きく向上しました。

1、LayaNative 1.0と比較する。


|         | 2D      | 3D       |
|------|---------------------|
|Android 124;を10%上げ90%向上させる
|IOS 124; 13%アップ270%アップ

2、国内の他の汎用runtimeエンジンと比較する。


|         | 2D       | 3D       |
|------|-----------------------|
|Android 124;は85%向上し90%向上します。
|IOS 124;を240%上げて270%上げます。

####拡張面で

1、LayaNative 2.0はシングルスレッドとダブルスレッドの2つのモードをサポートしていますが、開発者は自分のプロジェクトの実際のテスト結果に基づいて、どのモードを使うかを決めています。

-単スレッドモード：JSとRenderはスレッドで動作します。

−利点：動作に遅延がない（例えば、touch、キー）。
-欠点：性能はダブルスレッドモードに及ばない。

-ダブルスレッドモード：JSとRenderはそれぞれのスレッドで動作します。

-利点：性能はシングルスレッドバージョンよりも高い。
-欠点：操作は半フレームがあり、最大から一フレームまでの遅延（例えば、touch、ボタン）があります。

2、グラフィックカードのテクスチャの圧縮をサポートし、レンダリング効率を高めるだけでなく、現存の占用も減らすことができます。

3、最適化された二次開発は、より分かりやすく、開発者が使いやすいです。

####使いやすい面で、より便利なデバッグ機能を提供します。

**AndroidプラットフォームはJavaScriptを本格的にデバッグすることができます。**

LayaNative 1.0バージョンでは、デバッグ項目のJavaScriptコードは、consolie.logまたはalert関数のみを呼び出します。layaNative 2.0バージョンではChromeブラウザを使ってJavaScriptコードのデバッグを正式にサポートします。Chromeのコーディネーターでコードを断点的に追加したり、コード追跡したりする機能があります。

**テストアプリはスキャンコード起動項目に対応しています。**

開発者がより速くデバッグ開発ができるように、新しいバージョンのテストアプリにスキャンコード起動アプリの機能を追加しました。デバッグ時にマニュアルでURLを入力する手間を省きました。



##LayaCloud機能

LayaCloudは2.0のクラウドサービス解決方案で、開発者にユーザ認証（登録または授権など）、サーバデータアクセスと読み取り、部屋作成と管理、対戦マッチング、部屋内放送、フレーム同期などの基礎サービスを提供します。開発者はサーバの配置や負荷などに関心を持たず、LayaCloudが提供するAPIインターフェースを通じて、直接フロントエンドの開発言語を使って、オンラインゲームを簡単に実現します。複雑なサービスの要求に直面した場合、開発者は、クライアントで構成ファイルとサービスエンドの論理スクリプトを作成することによって、LayaCloudベースのAPIが提供できなかった機能または他のゲームビジネスロジックを実現することもできる。

LayaCloud技術文書ページ：https:/wiki.cloud.layabox.com/





詳細な2.0の新特性紹介についてはLayaboxのWeChat公式文章を確認できます。https://mp.weixin.qq.com/s/lH 3 tCozcFd_8fZ 1 PFJ 8 Xg



開発中にエンジンとツールのバグがある場合、またはコミュニティにアクセスして提出してください。http:/ask.layabox.com