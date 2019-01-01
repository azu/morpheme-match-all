# morpheme-match-all

A wrapper of [morpheme-match](https://github.com/azu/morpheme-match "morpheme-match") API. Match all kuromoji's tokens.

[kuromojin](https://github.com/azu/kuromojin "kuromojin")のtoken同士を比較して、
形態素解析結果を元にしたtoken辞書による比較を行うライブラリです。

## Install

Install with [npm](https://www.npmjs.com/):

    npm install morpheme-match-all

## Overview

morpheme-match-all compare two kuromoji's tokens using [morpheme-match](https://github.com/azu/morpheme-match "morpheme-match").

You can see kuromoji's tokens at [azu.github.io/morpheme-match/](https://azu.github.io/morpheme-match/ "morpheme-match").

### Dictionary

Define dictionary as `tokens` list.

```js
"use strict";
module.exports = [
    {
        // https://azu.github.io/morpheme-match/?text=解析(することができます)。
        message: `"することができる"は有害 http://qiita.com/takahi-i/items/a93dc2ff42af6b93f6e0`,
        tokens: [
            {
                "surface_form": "する",
                "pos": "動詞",
                "pos_detail_1": "自立",
                "pos_detail_2": "*",
                "pos_detail_3": "*",
                "conjugated_type": "サ変・スル",
                "conjugated_form": "基本形",
                "basic_form": "する",
                "reading": "スル",
                "pronunciation": "スル"
            },
            {
                "surface_form": "こと",
                "pos": "名詞",
                "pos_detail_1": "非自立",
                "pos_detail_2": "一般",
                "pos_detail_3": "*",
                "conjugated_type": "*",
                "conjugated_form": "*",
                "basic_form": "こと",
                "reading": "コト",
                "pronunciation": "コト"
            },
            {
                "surface_form": "が",
                "pos": "助詞",
                "pos_detail_1": "格助詞",
                "pos_detail_2": "一般",
                "pos_detail_3": "*",
                "conjugated_type": "*",
                "conjugated_form": "*",
                "basic_form": "が",
                "reading": "ガ",
                "pronunciation": "ガ"
            },
            {
                "pos": "動詞",
                "pos_detail_1": "自立",
                "conjugated_type": "一段",
                "conjugated_form": "連用形",
                "basic_form": "できる",
            }
        ]
    }
];
```

morpheme-match-all the actual tokens generated by [kuromojin](https://github.com/azu/kuromojin "kuromojin")([kuromoji.js](https://github.com/takuyaa/kuromoji.js "kuromoji.js")).

```js
const kuromojin = require("kuromojin");
const createMatcher = require("morpheme-match-all");
const dictionaries = require("./fixtures/dictionary");
const matchAll = createMatcher(dictionaries);
return kuromojin("解析することができます。").then((actualTokens) => {
    const results = matchAll(actualTokens);
    /**
[ { tokens: [ [Object], [Object], [Object], [Object] ],
index: 1,
expected: 
{ message: '"することができる"は有害 http://qiita.com/takahi-i/items/a93dc2ff42af6b93f6e0',
tokens: [Object] } } ]
     */
});
```

## Usage

<!-- Generated by documentation.js. Update this documentation by updating the source code. -->

#### Table of Contents

- [ExpectedDictionary][1]
  - [Properties][2]
- [MatchResult][3]
  - [Properties][4]
- [createMatcher][5]
  - [Parameters][6]
- [morphemeMatchAll][7]
  - [Parameters][8]

### ExpectedDictionary

Type: [Object][9]

#### Properties

- `tokens` **[Array][10]&lt;[Object][9]>** kuromoji's token list
- `message` **[string][11]?** 
- `expected` **[string][11]?** 

### MatchResult

Type: [Object][9]

#### Properties

- `tokens` **[Array][10]&lt;[Object][9]>** match tokens,
- `index` **[number][12]** index of first match token
- `skipped` **[Array][10]&lt;[boolean][13]>** skipped values for tokens
- `dict` **[Array][10]&lt;[ExpectedDictionary][14]>** dictionary defined by you

### createMatcher

#### Parameters

- `dictionaries` **[Array][10]&lt;[ExpectedDictionary][14]>** 

Returns **[morphemeMatchAll][15]** 

### morphemeMatchAll

match `actualTokens` with `dictionaries`

#### Parameters

- `actualTokens` **[Array][10]&lt;[Object][9]>** 

Returns **[Array][10]&lt;[MatchResult][16]>** 

[1]: #expecteddictionary

[2]: #properties

[3]: #matchresult

[4]: #properties-1

[5]: #creatematcher

[6]: #parameters

[7]: #morphemematchall

[8]: #parameters-1

[9]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object

[10]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array

[11]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String

[12]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Number

[13]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean

[14]: #expecteddictionary

[15]: #morphemematchall

[16]: #matchresult

## 参考

- [textlint-ja/textlint-rule-no-insert-dropping-sa: サ抜き、サ入れ表現の誤用をチェックするtextlintルール](https://github.com/textlint-ja/textlint-rule-no-insert-dropping-sa "textlint-ja/textlint-rule-no-insert-dropping-sa: サ抜き、サ入れ表現の誤用をチェックするtextlintルール")
- [textlint-ja/textlint-rule-ja-no-redundant-expression: 冗長な表現を禁止するtextlintルール](https://github.com/textlint-ja/textlint-rule-ja-no-redundant-expression "textlint-ja/textlint-rule-ja-no-redundant-expression: 冗長な表現を禁止するtextlintルール")

## Changelog

See [Releases page](https://github.com/azu/morpheme-match-all/releases).

## Running tests

Install devDependencies and Run `npm test`:

    npm i -d && npm test

## Contributing

Pull requests and stars are always welcome.

For bugs and feature requests, [please create an issue](https://github.com/azu/morpheme-match-all/issues).

1. Fork it!
2. Create your feature branch: `git checkout -b my-new-feature`
3. Commit your changes: `git commit -am 'Add some feature'`
4. Push to the branch: `git push origin my-new-feature`
5. Submit a pull request :D

## Author

- [github/azu](https://github.com/azu)
- [twitter/azu_re](https://twitter.com/azu_re)

## License

MIT © azu
