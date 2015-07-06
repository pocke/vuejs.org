title: FAQ
type: guide
order: 16
---

- **なぜ、Vue.js は IE8 をサポートしないのですか？**

  Vue.js は、ECMAScript 5 の新機能である `Object.defineProperty` メソッドを利用し、dirty check に頼ること無く、プレーンな JavaScript オブジェクトのシンタックスを提供することができます。IE8 において、このメソッドは DOM 要素にのみ有効で、JavaScript オブジェクトに対しては Polyfill ができないからです。

- **つまり、Vue.js はデータを上書きするのですか？**

  Vue.js は、規定のプロパティを getter と setter に変換するので、そのプロパティがアクセスまたは変更された場合には通知を受けることができます。シリアライズすると、データがまったく同じになります。もちろん、いくつかの注意点があります：

  1. `console.log` の出力では、getter/setter の束しか表示されません。しかし、`vm.$log()` を使うとさらに検出可能なログを出力できます。

  2. データオブジェクトに独自の getter/setter を定義することはできません。ただ、データオブジェクト自体はプレーンな JSON や Vue.js の computed properties から取得するので、これはあまり大した問題ではありません。

  3. Vue.js は、定義されたオブジェクトにいくつかのプロパティやメソッドを余分に追加します： `__ob__`、`$add`、`$set`、そして `$delete`。これらの特性は無数にあるので、`for ... in ...` のループには表示されません。しかし、それらを上書きした場合は、おそらく解除されます。

  だいたい以上です。オブジェクトのプロパティにアクセスしても `JSON.stringify` と `for ... in ...` ループは通常どおりに動作します。99.9% は、上記の配慮は必要ないでしょう。

- **Vue.js の現在の状況はどうですか？製品への使用はできますか?**

  Vue.js は、最新の 0.12 ではいくつかの API 変更を経てリリースされました。しかし、これは 1.0 以前の最後に計画されたポイントリリースです。その間にも、既に[プロダクションで Vue.js を使用している会社/プロジェクト](https://github.com/yyx990803/vue/wiki/Projects-Using-Vue.js) があります。

- **Vue.js の使用は無料でしょうか?**

  Vue.js は無料で使用でき、MIT ライセンスの下でソースを公開しています。

- **Vue.js と AngularJS の違いは何ですか？**

  何にでも当てはまるわけではないと思いますが、Angular の代わりに Vue を使用する理由がいくつかあります：

  1. Vue.js は、より柔軟で自己を主張しないライブラリと言えます。すべてにおいて Angular way を余儀なくされるのに対して、自分の好みのやり方でアプリを構築できます。本格的な SPA を作成せずとも、インターフェイス・レイヤーとしてページ内に軽度の機能実装を実現できるので、他のライブラリとの組み合わせを自由に選ぶ余地が生まれます。しかし、より多くのアーキテクチャ上の意思決定する責任があります。例えば、Vue.js のコアは、デフォルトでルーティングや ajax 機能が付属しておらず、そして通常は、外部モジュールバンドラを使用してアプリケーションを構築していると前提としています。これが、おそらく最も重要な違いと言えるでしょう。

  2. Vue.js は、API そして設計の両方の点から、Angular と比べて全体にとてもシンプルです。学習効率が非常に高いと言えます。

  3. Vue.js は、dirty check を行わないため優れたパフォーマンスを持っています。Angular は、スコープに変更がある度、すべてのウォッチャを評価し直すため、ウォッチャが多く存在すると遅くなりがちです。Vue.js は透過性依存的追跡を監視するシステムを採用しているので、明らかな依存関係が無い限りすべての変更のトリガは独立して機能し、この問題に悩まされることはありません。

  4. Vue.js では、コンポーネントは独自の View とデータロジックを持つ自己完結型のユニットであり、その中でディレクティブは様々な DOM 操作の紐付け（カプセル化）を行うものとして、両者の役割を明確に分離しています。Angular では、両者の使い分けに多くの曖昧な点が存在しています。

  しかし、Anguler は、Google がスポンサーとなり、実践で十分に証明され、最大規模のコミュニティがすでに存在しているのに対し、Vue.js はまだまだ比較的若いプロジェクトであることに注意してください。

- **Vue.js と React の違いは何ですか？**

  React.js と Vue.js は、どちらもリアクティブ＆コンポーザブルな View のコンポーネントを提供し、いくつかの類似性があります。しかし、内部実装は基本的に異なっています。React は、仮想 DOM 上で構築されます - 実際の DOM がどのように動作するかをメモリ内で表現しています。React 内のデータの大部分は不変で、DOM 操作は差分を算出して実行されます。それに引き換え、Vue.js はデフォルトでステートフルであり、内部のデータは変更可能です。変更はイベントを通じてトリガーされます。Vue.js は、仮想 DOM の代わりに実際の DOM をテンプレートとして使用し、データバインディングのために実際にノードへのリファレンスを保持します。

  仮想 DOM のアプローチは、任意のタイミングで View を描画する機能的な方法を提供します。オブザーバーを利用せず、更新ごとにアプリケーション全体を再描画しているため、View はデータと常に同期がされていることが保証されます。これは、他の JavaScript アプリケーションでも同様の可能性を与えることができます。 

  私自身は、全体的に React の設計思想の大ファンです。ただ、React における問題の一つがロジックと View が密に結びついていることです。一部の開発者にとっては恩恵になると思いますが、私のようなデザイナーと開発者のハイブリッドにとっては、テンプレートを持つことでデザインと CSS 設計を視覚的に捉えやすいものにしてくれます。JSX に JavaScript のロジックを組み合わせるのは、コードをデザインに変換していくための視覚的なモデル構造の邪魔になります。対照的に、Vue.js は、軽量な DSL (ディレクティブ) によりコストをかけており、そんために視覚的に構築可能なテンプレートと、ディレクティブとフィルタにカプセル化するロジックを持っています。

  React について別の問題を上げるなら、DOM の更新が完全に仮想 DOM に委任されていることです。実際に、DOM を**自分でコントロールする**のは少しトリッキーです（理論的には出来ますが、React の思想に反する結果になります）。複雑な時間の割り当てを行うアニメーションを実装する場合、これがかなり厄介な制限になることになります。この面では、Vue.js はより柔軟性があり、例として [multiple FWA/Awwwards winning sites](https://github.com/yyx990803/vue/wiki/Projects-Using-Vue.js#interactive-experiences) には Vue.js が組み込まれています。

- **Vue.js と Polymer との違いは何ですか?**
  Polymer はさらにもう1つの Google によってスポンサーされたプロジェクトで、実際には Vue.js も同様、インスピレーションの源でした。Vue.js のコンポーネントは Polymer のカスタム要素と比較して緩く、そして両方ともとても似た開発スタイルを提供します。最大の違いは、Polymer は最新の Web Components の機能に基づいて構築されており、そしてネイティブにこれらの機能をサポートしていないブラウザでは動作せるために(パフォーマンス低下)、ささいでない polyfills を必要します。これとは対照的に、Vue.js は IE9 まで依存せずに動作します。

- **Vue.js と KnockoutJS の違いは何ですか?**

  まず、Vue は VM(ViewModel) プロパティの取得や設定で、クリーンな構文を組みやすいという点があります。

  より高いレベルでは、Vue のコンポーネントシステムはトップダウン設計による手続き型の設計戦略に基づき、まずシステム全体を定義します。対して Knockout は、オブジェクト指向言語で主流のボトムアップ設計に基づき、個々の ViewModel を組み上げてシステムを構成していきます。Vue において、ソースデータはプレーンなロジックレスのオブジェクトです（つまり、直接 `JSON.stringify()` を使い POST リクエストを投げることが出来ます）。ViewModel は、単にそのデータへプロキシ経由でアクセスするものです。Vue の VM インスタンスは、常に対応する DOM 要素に生データを接続している状態になります。Knockout では、ViewModel は本質的に**データそのもの**であり、Model と ViewModel の境界はかなり曖昧なものになっています。この点で、Knockout はさらなる柔軟性を獲得していますが、同時にはるかに複雑な ViewModel の構造をもたらす可能性が高いです。

- **ぜひ、協力を！**
コントリビューションガイドを読んで、<a href="https://gitter.im/yyx990803/vue" target="_blank"><img src="https://badges.gitter.im/Join%20Chat.svg"></a> の議論に参加しましょう！