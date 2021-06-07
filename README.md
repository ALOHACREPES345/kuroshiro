![kuroshiro](https://kuroshiro.org/kuroshiro.png)

# kuroshiro

[![Build Status](https://travis-ci.org/hexenq/kuroshiro.svg?branch=master)](https://travis-ci.org/hexenq/kuroshiro)
[![Coverage Status](https://coveralls.io/repos/hexenq/kuroshiro/badge.svg)](https://coveralls.io/r/hexenq/kuroshiro)
[![npm version](https://badge.fury.io/js/kuroshiro.svg)](http://badge.fury.io/js/kuroshiro)
[![Join the chat at https://gitter.im/hexenq/kuroshiro](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/hexenq/kuroshiro)
[![License](https://img.shields.io/github/license/lassjs/lass.svg)](LICENSE)

kuroshiro is a Japanese language library for converting Japanese sentence to Hiragana, Katakana or Romaji with furigana and okurigana modes supported.

*Read this in other languages: [English](README.md), [日本語](README.jp.md), [简体中文](README.zh-cn.md), [繁體中文](README.zh-tw.md), [Esperanto](README.eo-eo.md).*

## Demo
*For convenience, this demo utilizes Yahoo-WebAPI analyzer plugin. However this analyzer might not give optimized converted result when converting kanji to romaji with kuroshiro since Yahoo Web API lacks information of pronunciation in analysis result. Use other analyzer plugins could avoid this issue. Please note that.*
<style>    
    #demoArea {
        font-size: 16pt;
    }
    .submitBtn {
    display: inline-block;
    -webkit-box-sizing: content-box;
    -moz-box-sizing: content-box;
    box-sizing: content-box;
    margin: 0.6em 0 0.5em 0;
    padding: 0 1.5em;
    border: 1px solid rgba(211,211,211,1);
    -webkit-border-radius: 0.2em;
    border-radius: 0.2em;
    font: normal normal bold 1em/1.5em Arial, Helvetica, sans-serif;
    color: rgba(114,114,114,1);
    -o-text-overflow: clip;
    text-overflow: clip;
    white-space: nowrap;
    background: rgba(234,234,234,1);
    -webkit-box-shadow: 0 0 1px 1px rgba(255,255,255,0.8) , 0 1px 0 0 rgba(0,0,0,0.298039) ;
    box-shadow: 0 0 1px 1px rgba(255,255,255,0.8) , 0 1px 0 0 rgba(0,0,0,0.298039) ;
    text-shadow: 0 1px 0 rgba(255,255,255,0.8) ;
    -webkit-transition: all 200ms cubic-bezier(0.42, 0, 0.58, 1) 10ms;
    -moz-transition: all 200ms cubic-bezier(0.42, 0, 0.58, 1) 10ms;
    -o-transition: all 200ms cubic-bezier(0.42, 0, 0.58, 1) 10ms;
    transition: all 200ms cubic-bezier(0.42, 0, 0.58, 1) 10ms;
    }

    .submitBtn:hover {
    cursor: pointer;
    border: 1px solid rgba(178,178,178,1);
    color: rgba(76,76,76,1);
    -webkit-box-shadow: 0 0 1px 1px rgba(255,255,255,0.8) inset, 0 1px 0 0 rgba(0,0,0,0.298039) ;
    box-shadow: 0 0 1px 1px rgba(255,255,255,0.8) inset, 0 1px 0 0 rgba(0,0,0,0.298039) ;
    }

    .submitBtn:active {
    position: relative;
    cursor: default;
    top: 1px;
    border: 1px solid rgba(211,211,211,1);
    color: rgba(114,114,114,1);
    background: rgba(247,247,247,1);
    -webkit-box-shadow: 0 0 1px 1px rgba(255,255,255,0.8) inset, 0 1px 0 0 rgba(0,0,0,0.298039) inset;
    box-shadow: 0 0 1px 1px rgba(255,255,255,0.8) inset, 0 1px 0 0 rgba(0,0,0,0.298039) inset;
    -webkit-transition: none;
    -moz-transition: none;
    -o-transition: none;
    transition: none;
    }

    select {
    -webkit-appearance: none;
    -moz-appearance: none;
    -ms-appearance: none;
    appearance: none;
    outline: 0;
    box-shadow: none;
    border: 0 !important;
    background: #eaeaea;
    background-image: none;
    }
    /* Custom Select */
    .select {
    vertical-align: bottom;
    position: relative;
    display: inline-block;
    width: 5em;
    height: 1.4em;
    line-height: 1em;
    background: #eaeaea;
    overflow: hidden;
    border-radius: .25em;
    }
    select {
    width: 100%;
    height: 100%;
    margin: 0;
    padding: 0 0 0 .5em;
    color: #727272;
    cursor: pointer;
    font-size: 0.8em;
    }
    select::-ms-expand {
    display: none;
    }
    /* Arrow */
    .select::after {
    content: '\25BC';
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    padding: .3em .3em .2em;
    background: #eaeaea;
    pointer-events: none;
    font-size: .6em;
    color: #727272;
    }
    /* Transition */
    .select:hover::after {
    color: #727272;
    }
    .select::after {
    -webkit-transition: .25s all ease;
    -o-transition: .25s all ease;
    transition: .25s all ease;
    }

    .option {
        display: inline-block;
        margin-right: 1em;
    }
</style>
<div id="demoArea">
    <label>Original Text:</label>
    <div>
        <textarea id="oritext" style="width:100%;border-radius: .2em;font-size: 1em;" rows="8">感じ取れたら手を繋ごう、重なるのは人生のライン and レミリア最高！</textarea>
    </div>
    <div class="option">
        <label>To </label>
        <div class="select">
            <select id="to" name="to" tabindex="2">
                <option value="hiragana" selected="">Hiragana</option>
                <option value="katakana">Katakana</option>
                <option value="romaji">Romaji</option>
            </select>
        </div>
    </div>
    
    <div class="option">
        <label> Mode </label>
        <div class="select">
            <select id="mode" name="mode" tabindex="1">
                <option value="normal" selected="">Normal</option>
                <option value="spaced">Spaced</option>
                <option value="okurigana">Okurigana</option>
                <option value="furigana">Furigana</option>
            </select>
        </div>
    </div>    
    <div id="romajiOption" class="option" style="display:none">
        <label> Romaji System </label>
        <div class="select">
            <select id="romajiSystem" name="romajiSystem" tabindex="3">
                <option value="nippon" selected="">Nippon</option>
                <option value="passport">Passport</option>
                <option value="hepburn">Hepburn</option>
            </select>
        </div>
    </div>    
    <br />
    <button id="convertBtn" class="submitBtn" onclick="convert()">convert</button>
    <div>
        <p id="output"></p>
    </div>
</div>
<script>
    document.addEventListener('DOMContentLoaded',function() {
        document.getElementById('to').onchange=function(evt){
            if(evt.target.value == "romaji"){
                document.getElementById("romajiOption").setAttribute("style","display:inline-block");
            }else{
                document.getElementById("romajiOption").setAttribute("style","display:none");
            }
        };
    },false);
    
    function convert(){
        document.getElementById("convertBtn").textContent="converting...";
        document.getElementById("convertBtn").disabled=true;
        fetch("https://api.kuroshiro.org/convert",{
            method: 'POST',
            headers: {
                'Content-Type': 'application/json;charset=UTF-8'
            },
            body: JSON.stringify({
                str: document.getElementById("oritext").value,
                to:document.getElementById("to").value,
                mode:document.getElementById("mode").value,
                romajiSystem:document.getElementById("romajiSystem").value
            })
        })
            .then((resp)=>{
                if(resp.ok){
                    return resp.json();
                }else if(resp.status == 429){
                    document.getElementById("output").innerHTML = "<p>Error:</p>" + "Too many request. Please try again later.";
                    throw new Error("Too many request");
                }else{
                    document.getElementById("output").innerHTML = "<p>Error:</p>" + "Something wrong. Please try again later.";
                    throw new Error("Something wrong");
                }
            })
            .then((result)=>{
                document.getElementById("output").innerHTML = "<p>Result:</p>" + result.result;
                document.getElementById("convertBtn").textContent="convert";
                document.getElementById("convertBtn").disabled=false;
            })
            .catch((err)=>{
                console.error(err);
                document.getElementById("output").innerHTML = "<p>Error:</p>" + "Something wrong. Please try again later.";
                document.getElementById("convertBtn").textContent="convert";
                document.getElementById("convertBtn").disabled=false;
            })
    }
</script>

## Feature
- Japanese Sentence => Hiragana, Katakana or Romaji
- Furigana and okurigana supported
- 🆕Multiple morphological analyzers supported
- 🆕Multiple romanization systems supported
- Useful Japanese utils

## Breaking Change in 1.x
- Seperate morphological analyzer from phonetic notation logic to make it possible that we can use different morphological analyzers ([ready-made](#ready-made-analyzer-plugins) or [customized](CONTRIBUTING.md#how-to-submit-new-analyzer-plugins))
- Embrace ES8/ES2017 to use async/await functions
- Use ES6 Module instead of CommonJS
    
## Ready-made Analyzer Plugins
*You should check the environment compatibility of each analyzer before you start working with them*

| Analyzer      | Node.js Support | Browser Support | Plugin Repo                                                                                  | Developer                             |
| ------------- | --------------- | --------------- | -------------------------------------------------------------------------------------------- | ------------------------------------- |
| Kuromoji      | ✓               | ✓               | [kuroshiro-analyzer-kuromoji](https://github.com/hexenq/kuroshiro-analyzer-kuromoji)         | [Hexen Qi](https://github.com/hexenq) |
| Mecab         | ✓               | ✗               | [kuroshiro-analyzer-mecab](https://github.com/hexenq/kuroshiro-analyzer-mecab)               | [Hexen Qi](https://github.com/hexenq) |
| Yahoo Web API | ✓               | ✗               | [kuroshiro-analyzer-yahoo-webapi](https://github.com/hexenq/kuroshiro-analyzer-yahoo-webapi) | [Hexen Qi](https://github.com/hexenq) |

## Usage
### Node.js (or using a module bundler (e.g. Webpack))
Install with npm package manager:
```sh
$ npm install kuroshiro
```

Load the library:

*Support ES6 Module `import`*
```js
import Kuroshiro from "kuroshiro";
// Initialize kuroshiro with an instance of analyzer (You could check the [apidoc](#initanalyzer) for more information):
// For this example, you should npm install and import the kuromoji analyzer first
import KuromojiAnalyzer from "kuroshiro-analyzer-kuromoji";
// Instantiate:
const kuroshiro = new Kuroshiro();
// Initialize
// Here uses async/await, you could also use Promise
await kuroshiro.init(new KuromojiAnalyzer());
// Convert what you want:
const result = await kuroshiro.convert("感じ取れたら手を繋ごう、重なるのは人生のライン and レミリア最高！", { to: "hiragana" });
```

*And CommonJS `require`*

```js
const KuromojiAnalyzer = require("kuroshiro-analyzer-kuromoji");
const Kuroshiro = require("kuroshiro")
const kuroshiro = new Kuroshiro();

kuroshiro.init(new KuromojiAnalyzer())
.then(function () {
    return kuroshiro.convert("シンゲキ ノ キョジン", {to: "romaji"});
})
.then(function(result){
  console.log(result);
  //shingeki no kyojin
})
```
    
### Browser
Add `dist/kuroshiro.min.js` to your frontend project (you may first build it from source with `npm run build` after `npm install`), and in your HTML:
```html
<script src="url/to/kuroshiro.min.js"></script>
```

For this example, you should also include `kuroshiro-analyzer-kuromoji.min.js` which you could get from [kuroshiro-analyzer-kuromoji](https://github.com/hexenq/kuroshiro-analyzer-kuromoji)
```html
<script src="url/to/kuroshiro-analyzer-kuromoji.min.js"></script>
```

Instantiate:
```js
var kuroshiro = new Kuroshiro();
```

Initialize kuroshiro with an instance of analyzer, then convert what you want:
```js
kuroshiro.init(new KuromojiAnalyzer({ dictPath: "url/to/dictFiles" }))
    .then(function () {
        return kuroshiro.convert("感じ取れたら手を繋ごう、重なるのは人生のライン and レミリア最高！", { to: "hiragana" });
    })
    .then(function(result){
        console.log(result);
    })
```

## API
### Constructor
__Examples__

```js
const kuroshiro = new Kuroshiro();
```

### Instance Medthods
#### init(analyzer)
Initialize kuroshiro with an instance of analyzer. You should first import an analyzer and initialize it. You can make use of the [Ready-made Analyzers](#ready-made-analyzer-plugins) listed above. And please refer to documentation of analyzers for analyzer initialization instructions

__Arguments__

* `analyzer` - An instance of analyzer.

__Examples__

```js
await kuroshiro.init(new KuromojiAnalyzer());
```

#### convert(str, [options])
Convert given string to target syllabary with options available

__Arguments__

* `str` - A String to be converted.
* `options` - *Optional* kuroshiro has several convert options as below.

| Options                  | Type   | Default    | Description                                                |
| ------------------------ | ------ | ---------- | ---------------------------------------------------------- |
| to                       | String | "hiragana" | Target syllabary [`hiragana`, `katakana`, `romaji`]        |
| mode                     | String | "normal"   | Convert mode [`normal`, `spaced`, `okurigana`, `furigana`] |
| romajiSystem<sup>*</sup> | String | "hepburn"  | Romanization system [`nippon`, `passport`, `hepburn`]      |
| delimiter_start          | String | "("        | Delimiter(Start)                                           |
| delimiter_end            | String | ")"        | Delimiter(End)                                             |

**: Param `romajiSystem` is only applied when the value of param `to` is `romaji`. For more about it, check [Romanization System](#romanization-system)*

__Examples__

```js
// normal
await kuroshiro.convert("感じ取れたら手を繋ごう、重なるのは人生のライン and レミリア最高！", {mode:"okurigana", to:"hiragana"});
// result：かんじとれたらてをつなごう、かさなるのはじんせいのライン and レミリアさいこう！
```

```js
// spaced
await kuroshiro.convert("感じ取れたら手を繋ごう、重なるのは人生のライン and レミリア最高！", {mode:"okurigana", to:"hiragana"});
// result：かんじとれ たら て を つなご う 、 かさなる の は じんせい の ライン   and   レミ リア さいこう ！
```

```js
// okurigana
await kuroshiro.convert("感じ取れたら手を繋ごう、重なるのは人生のライン and レミリア最高！", {mode:"okurigana", to:"hiragana"});
// result: 感(かん)じ取(と)れたら手(て)を繋(つな)ごう、重(かさ)なるのは人生(じんせい)のライン and レミリア最高(さいこう)！
```

<pre>
// furigana
await kuroshiro.convert("感じ取れたら手を繋ごう、重なるのは人生のライン and レミリア最高！", {mode:"furigana", to:"hiragana"});
// result: <ruby>感<rp>(</rp><rt>かん</rt><rp>)</rp></ruby>じ<ruby>取<rp>(</rp><rt>と</rt><rp>)</rp></ruby>れたら<ruby>手<rp>(</rp><rt>て</rt><rp>)</rp></ruby>を<ruby>繋<rp>(</rp><rt>つな</rt><rp>)</rp></ruby>ごう、<ruby>重<rp>(</rp><rt>かさ</rt><rp>)</rp></ruby>なるのは<ruby>人生<rp>(</rp><rt>じんせい</rt><rp>)</rp></ruby>のライン and レミリア<ruby>最高<rp>(</rp><rt>さいこう</rt><rp>)</rp></ruby>！
</pre>

### Utils
__Examples__
```js
const result = Kuroshiro.Util.isHiragana("あ"));
```
#### isHiragana(char)
Check if input char is hiragana.

#### isKatakana(char)
Check if input char is katakana.

#### isKana(char)
Check if input char is kana.

#### isKanji(char)
Check if input char is kanji.

#### isJapanese(char)
Check if input char is Japanese.

#### hasHiragana(str)
Check if input string has hiragana.

#### hasKatakana(str)
Check if input string has katakana.

#### hasKana(str)
Check if input string has kana.

#### hasKanji(str)
Check if input string has kanji.

#### hasJapanese(str)
Check if input string has Japanese.

#### kanaToHiragna(str)
Convert input kana string to hiragana.

#### kanaToKatakana(str)
Convert input kana string to katakana.

#### kanaToRomaji(str, system)
Convert input kana string to romaji. Param `system` accepts `"nippon"`, `"passport"`, `"hepburn"` (Default: "hepburn").

## Romanization System
kuroshiro supports three kinds of romanization systems.

`nippon`: Nippon-shiki romanization. Refer to [ISO 3602 Strict](http://www.age.ne.jp/x/nrs/iso3602/iso3602.html).

`passport`: Passport-shiki romanization. Refer to [Japanese romanization table](https://www.ezairyu.mofa.go.jp/passport/hebon.html) published by Ministry of Foreign Affairs of Japan.

`hepburn`: Hepburn romanization. Refer to [BS 4812 : 1972](https://archive.is/PiJ4).

There is a useful [webpage](http://jgrammar.life.coocan.jp/ja/data/rohmaji2.htm) for you to check the difference between these romanization systems.

### Notice for Romaji Conversion
Since it's impossible to fully automatically convert __furigana__ directly to __romaji__ because furigana lacks information on pronunciation (Refer to [なぜ フリガナでは ダメなのか？](https://green.adam.ne.jp/roomazi/onamae.html#naze)). 

kuroshiro will not handle chōon when processing directly furigana (kana) -> romaji conversion with `nippon` or `hepburn` romanization system (Chōon will be ignored by `passport` romanization system) 

*For example, you'll get "kousi", "koshi", "koushi" respectively when converts kana "こうし" to romaji 
using `nippon`, `passport`, `hepburn` romanization system.*

The kanji -> romaji conversion with/without furigana mode is __unaffected__ by this logic.

## Contributing
Please check [CONTRIBUTING](CONTRIBUTING.md).

## Inspired By
- kuromoji
- wanakana

## License
MIT
