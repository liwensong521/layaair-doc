#音楽とサウンドの再生とコントロール

HTML 5のオーディオ再生は、現在は2つの主流の方式があります。1つはAudioタグ再生、もう1つはWebAudioバイナリ再生です。

Audioはdom要素に属し、uiインタフェースを持ち、モバイル端末Audioはダウンロードしながら再生し、音声ファイルの大きいファイルに適していますが、Audioはモバイル端末でジェスチャーの制限があります。

WebAudioは、複数の音声をロードして合成することができる新しい音声再生形態であり、バイナリファイルを通じてブラウザサポートのフォーマットにデコードして再生する。また、このインターフェイスを使ってオーディオスペクトルの動画効果を実現し、音声を合成する機能を持つようになりました。

音楽とサウンドはゲームでよく使われる基本的な要素として、LayaAirエンジンはWebAudioとAudioをパッケージ化しています。WebAudioをサポートするブラウザでは、WebAudioを優先的に使用し、WebAudioをサポートしないブラウザでAudioを使用しています。最大化はすべてのブラウザに対応しています。口から直接オーディオを再生できます。

###一、音楽と音効の応用の違い

音楽：ゲーム用のBGMです。laya.media.SoundManagerオーディオ管理クラスのplayMusic方式で再生します。背景音楽ですので、playMusic方式はオーディオファイルを同時に再生するしかありません。

サウンド：laya.media.SoundManagerオーディオ管理クラスのplaySoundメソッドを採用しており、複数のオーディオファイルを同時に再生することができます。

###二、オーディオの互換性の準備

音声再生の問題は各ブラウザの互換性が違っていますので、アプリケーションを開始する前に、前期の互換性を準備しておきます。

（1）「フォーマット工場」オーディオファイル変換ツールを使用します。44100 Hzを選択し、96 kbpsを変換します。

（2）オーディオファイルは、帯域幅の制限だけでなく、ブラウザの音声復号の効率に問題がある。

###三、オーディオ音量の制御

音量の制御はlaya.media.SoundManagerオーディオ管理クラスのsetSoundVolumeメソッドで設定できます。

![blob.png](http://old.ldc.layabox.com/uploadfile/image/20170110/1484019651349259.png)

上記のように、volumeパラメータを設定することで、urlに対応する音声ファイルの音量を効果的に制御することができます。初期値は1です。音量範囲は0(ミュート)から1(最大音量)までです。



###四、設備の静音制御

デバイスのミュートキーを押すと、自動的にオーディオがデバイスのミュートに従います。useAudioMusicをfalseに設定する必要があります。


```javascript

SoundManager.useAudioMusic=false；
```




###五、音楽とサウンド再生の完全な例

この例の完全コードアドレスは以下の通りです。[https://layaair.ldc.layabox.com/demo/?2d&Sound&SimpleDemo](https://layaair.ldc.layabox.com/demo/?2d&Sound&SimpleDemo)