# 「最近のDMMのフロントエンドの動向とその先について」@ur_uha 千葉

* CTO室 Webエンジニア
* 体制とフロントエンドの関わり
* 技術展開
* 現状の課題と今後

## 今

* 事業部制
* CTO室: 事業部支援、制度支援、啓蒙活動、SRE、炎上対応、smartcontract,ai のM&A

* scrum

* 良い意味で責務が崩壊
* AWSやGCPを日常的に触るFEも増えた

## 昔

* デザイン本部・システム本部という横断組織
* コミュニケーションレス（フロントエンド・サーバサイドの責務が別れている）
  * 職種レイヤー間でのコミュニケーションロス
  * 出戻りやレイヤーを超えた修正に時間かかる

## TECH VISION

* CTO松本（昨年からジョイン）
* 20年超えサービスの負債
* jQuery1系、node4系
* サーバサイドのテンプレートエンジンと密結合

* tech blog読め

* frontend backend を疎にしているところ

## ここ数年で使われ始めた

* React, Vue
  * 事業に合わせて取捨選択

## 課題

* 圧倒的人材不足
  * Webアプリケーション全体を俯瞰した上でフロントエンドにアプローチできる人材が少ない

# 「FlashアプリケーションをHTML5 アプリケーションにリプレイスしている話」@norih_7 萩原

* 2012年入社

* ライブ配信Flashアプリケーションのリプレース
  * 2018年4月頃から10人前後で

* webrtc(映像)
* websocket(comunication)
* react, redux(ui)

* flash player 2020 年にサポート終了
* 古いアプリケーションで保守・拡張が難しい

* スクラム開発

* 難しい問題にチームで立ち向かえる
  * webrtc により問題が散見
  * ペアプロ、モブプロにより解決・効率上昇

* 小さいサイクル、レトロスペクティブ
  * スプリントは1週間
  * まずは作って改善
  * レトロスペクティブでの建設的な改善
  * 軌道に乗るまでは大変

* 2018/7 チーム分け
  * 開発がうまく進まない
    * スピードが出ない
  * パフォーマンスを挙げられた
    * プロフェッショナル志向に沿っている：モチベ高い
    * 意思決定・実装早い・品質高い

* 2018/12 - 2019/3
  * 小さいサービスリリースで実験
    * 技術的な不安の実験
      * webrtc配信システムが社外のユーザ環境で利用可能か
    * 既存システムとの依存関係を最低限

* 2019/4-
  * 新規アプリケーション開発

* フロントエンド開発について
  * タスク量多い

* テストを書く
  * jest
  * enzyme で react コンポーネントの単体テスト

* コードフォーマットの統一

* 新規デプロイシステムの構築
  * aws と ciで配信サーバとデプロイシステムの構築

* ログ管理
  * ログ調査大変。属人化。必要なログ収集できていない
  * elasticsearch
  * sentry

* uiのカタログ化と再利用

* 困ったこと
  * windowsのブラウザでアプリが動かない
    * 社外からの配信テストで気づき
    * windows は機種によってコントロールパネルから許可設定が必要
    * 社外での実地検証大事
  * pub/subの複数アプリケーション
    * パッケージ化:きつい
    * monorepo化で乗り切った
  * デザイナとの連携
    * 開発チームにデザイナがいない
    * 静的なHTMLとCSSを作ってもらい、JSXで実装
    * オープンなコミュニケーションで克服(SLACK)
    * まだ改善中


# 「Nuxt.jsをLPジェネレーターとして使ってみた話」清宮

* nuxt.jsを単なるジェネレータとして使うならここに気をつけようぜ
* エンターテインメント開発部
  * FEがいない/足りない部署のweb制作実施

* 全体の工数の1/3がLP作成
* いわゆるペライチ
* HTML, Sass, ES6
* LP制作は環境構築に時間がかかる

* 良いStaticSiteGeneratorを探せ！！！
  * それまではnpm_scriptsをカスタマイズしていた

* 基準
  * FEなのでNode.jsで動く
  * ドキュメントやブログに特化したものを除外: vuepress, gitbook
  * ssrやpwaなどの応用もききそう-> nuxt
    * 波に乗っかる
    * チーム内ナレッジはvueが強かった
    * 試して合わなかったら別のためそうか、のような

* メリデメ

* メリ
  * コスト削減
    * css設計コスト下がる
    * レビューもやりやすい
  * 手軽
    * api経由の際データをバインディングしてくれる
    * 複数ページでもrouting可
    * cssをscpoed / module で影響範囲限定

* デメ
  * コスト増えた
    * サーバサイドで PC/SP 判別の際の意図しないrouting
    * DOMをいじるモジュールを読み込む必要があるときは面倒
    * 動きのあるLPを実現するためのplugin調査(一時的)
  * その他断念したケース
    * 納品先で運用が走る場合、向こうのスキルセットに依存するのでやめた

* Nuxt.jsでLPを作る際に向いているかどうか判断基準
  * 運用が発生しない / 発生しても対応できる
  * サーバサイドのフレームワークを使用していない（該当箇所のみの適用を回避できる）
  * 動的なDOM変更を外部モジュール等で行っていない
  * 複雑なアニメーションで使いたいLibraryがすぐに浮かぶ場合
  * 初期学習済み / 学習コストをかけても大丈夫

* matchケース
  * apiをたくさんたたく / HeadlessCMSなLP
  * 同じようなページ構造でいくつかのLPを作るようなケース
  * レスポンシブなLP

# 「Nuxt.jsによる新規開発」上井