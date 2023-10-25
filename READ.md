<h1>10月：積み上げ</h1>
<ul>
    <ol>暗記はするな。概念などをまとめよう。</ol>
    <ol>できるだけ自分の言葉でまとめよう。</ol>
    <ol>参考記事はできるだけエビデンスを担保するために、2つ以上集める</ol>
</ul>

## "2023 10.01"
git push origin master でのエラー対応

対象ファイル：https://github.com/tkg-reis/new_gulp_sass_img_js

<p>
原因：以前に、上記からgit clone もしくは git pull の操作をした際に、Github上のファイルとローカルのファイルの中身が一致しない現象を引き起こした可能性が高い。
</p>

<p>
解決：エラーメッセージと参照記事からgit pull origin master を実行することでGithub上の最新ファイルをローカルファイルに更新できる。
</p>

ref
https://zenn.dev/yuma_rails/articles/4cfde6a523a72e

### TypeScript intersection types

2つの型宣言がある場合、typeで型宣言をして、それらを結合する操作。結合する場合、type宣言して定義した型ともう一方の型をアンバサンド&で結合する。
ex. type User = Profile & Login

### TypeScript union types
ある変数などに対して、型を二つ定義したいときに使用する。論理和の|を使用して定義する。
ex. let val : boolean | string;
    let array: (boolean | string)[];

### TypeScript literal types
ある変数に代入できる者を限定することが可能。（文字列、数字でも可能）
ex. let company : "Facebook" | "Twitter" | "Apple" ;
    company = "Facebook";
    company = "amazon"は代入不可

### TypeScript typeof 
ある宣言済みの変数などに定義された型を別の変数の型に継承するやり方。宣言済みの変数の型以外の型のものを代入するとエラーになる。宣言済みかどうかは型推論できているかどうか。オブジェクト形式の型も継承可能。
ex. let msg: string = "Hello"
    let talk: typeof msg;

### TypeScript keyof 
キー情報を型で定義して、そのキーをユニオン型で継承して使用するキーの部分の型宣言。
ex. type Keys = { primary: string, secondary: string}
    let keys :keyof : Keys 
    key = primary 


### keyof + typeof
ex. const Sport = {
    soccer: "soccer",
    baseball: "baseball",
}

let keySports: keyof typeof Sport
型とキー情報を継承して使用することが可能。

### TypeScript enum
オブジェクトのキーだけのように記述。自動で連番を割り当ててくれるので、バグを防ぐことができる。
enum OS {
    Windows,
    Mac,
    Linux
}

interface PC {
    id: number;
    OSType: OS;
}

const PC: PC = {
    id: 1,
    OSType: OS.Windows
}

<hr>

## "2023 10.03"
### useReducer

分からない部分：useStateとuseReducerの違い。

理解したこと：処理条件を複数設置することが可能になる。dispatch関数を実行することで、useReducerの第一引数の処理が実行される。

ref
https://qiita.com/hibi_toshi/items/ad5b79f20547d5eb8d05?utm_campaign=post_article&utm_medium=twitter&utm_source=twitter_share&s=09
https://reffect.co.jp/react/react-hook-reducer-understanding/


<hr>

## "2023.10.11"
### Generics

先にインターフェースの形だけを作っておく。
<T>はよく使われるエイリアス。<T>に型が渡るイメージ。

interface Gen<T> {
    item: T;
};

後からitemの型を当てはめる。

const gen0:Gen<string> = {
    item: "hello"
};

また、デフォルトで型を定義することも可能。

interface Gen1<T = string> {
    item: T;
}

const gen1: Gen1 = {
    item: "hello"
};

また型を動的に指定することも可能。型の事前指定。

interface Gen2<T extends string | number> {
    item: T;
}

const gen2: Gen2<string> = {
    item: "hello"
}

関数の引数でも型を指定する。
function funcGen1<T>(props: T) {
    return {item : props}
}

型推論が働くので、型を明示的に宣言する必要がない
const gen3 = funcGen1("test")
funcGen1<string>("test")

上記は同義である。

ユニオン型を使用しても型を付けられる。
const gen4 = funcGen<string | null>(null);

function funcGen2<T extends string | null>(props: T) {
    return {val: props }
}

const gen5 = funcGen2("test2");

interfaceとextendsで型を事前に指定することも可能。

interface Props {
    price: number;
}

function funcGen3<T extends Props>(props: T) {
    return {
        val: props.price
    }
};

const gen6 = funcGen3({price: 12});

#### アロー関数での書き方

const funcGen4 = <T extends Props>(props: T) => {
    return {
        val: props.price
    }
}

## Java Public static void main(String[] args)の意味

わかったこと：argsはargumentの略（引数）。JavaとJavaScriptはそもそもの実行動作が違う気がする。
対話型と非対話型言語の調査。Javaはコンパイラ言語、JavaScriptはインタープリタ言語（スクリプト言語）である。

ref
<code>
https://qiita.com/kahatato/items/1b4921bb58731f0b7fea#:~:text=%E3%81%AE%E7%95%A5%E7%9C%81-,args%E3%81%AB%E3%81%A4%E3%81%84%E3%81%A6,%E5%8F%97%E3%81%91%E7%B6%99%E3%81%84%E3%81%A7%E3%81%84%E3%82%8B%E3%81%9F%E3%82%81%E3%81%A7%E3%81%99%E3%80%82
</code>

## コンパイラ言語とインタープリタ言語

結論：前者は、プログラムの実行時に、PCが読める文字に変更を加える。ソースプログラムをいったん機械語に翻訳し，その機械語になったプログラムを実行する方式。実行速度は早い。実行時に文字変更を加える関係で、コンパイラしないとエラーが出てこない。
ex.C++・Objective-C・Go・swift・(Java)

後者は、あらかじめPCが読める文字に変更すること。命令を一つずつ，機械語に解釈しながら実行する方式。実行速度は割と遅い。命令1つに対してなので、エラーの発見がしやすい。
ex.HTMLやCSS・Ruby・Python・JavaScript・PHP

Javaは双方の中間的な存在。

ref
<code>
<ul>
    <li>
        https://www.zealseeds.com/Lang/LangJavascript/WhatIsJavaScript/index.html#jump3
    </li>
    <li>
        https://www3.cuc.ac.jp/~miyata/classes/prg1/02/2way.html
    </li>
    <li>
        https://www.tokai-bs.co.jp/trends/column-350/#:~:text=%E3%82%A4%E3%83%B3%E3%82%BF%E3%83%BC%E3%83%97%E3%83%AA%E3%82%BF%E5%9E%8B%E8%A8%80%E8%AA%9E%E3%81%AE%E4%BE%8B,%E3%82%89%E3%82%8C%E3%82%8B%E3%81%93%E3%81%A8%E3%81%8C%E5%A4%9A%E3%81%8F%E3%81%82%E3%82%8A%E3%81%BE%E3%81%99%E3%80%82
    </li>
</ul>

</code>

## "23.10.15"
### 追記 JavaScript/TypeScriptの各言語タイプ

結論：JavaScript/TypeScriptを触っていれば、理解がしやすい！！

Javascriptはインタープリター言語、TypeScriptはコンパイラ言語である。前者はブラウザで即実行されるのではやい！後者はコンパイルしないと使用できない。かつtscのインストールの手間やtscコマンドで、コンパイル処理しないといけないので面倒。だが型が付くので開発に適している。

ref
<code>
    https://xtech.nikkei.com/atcl/nxt/column/18/02450/051900002/
</code>

<code>
    https://webpia.jp/interpreter-merit/
</code>

<hr>

## "23.10.12"

### jsonの型推論

結論：jsonのデータをtypeofで型指定すると、自動で型推論が働き、型の直に打つ作業がなくなる。

<code>
    import Data from './data';
    type User = typeof Data;
</code>

<hr>

## "23.10.15"

### Javaのファイル間の情報の受け渡し方について

結論：import.パッケージ名.subDir.参照するクラスの名前。こうすることで、オブジェクト指向開発ができる。

ref
<code>
    https://style.potepan.com/articles/31604.html
</code>

<hr>

## "23.10.16"

### ブラウザレンダリングの仕組み

結論：html=> (bytes=> chars => token => nodes => DOM) => css解析(厳密にはlinkがhtmlで見つかったとき) => (bytes=> chars => token => nodes => cssOM) => JavaScript =>(compile) => make render tree => layout => painting(画面に描画していく行程) => 

ref 
<code>https://zenn.dev/ak/articles/c28fa3a9ba7edb</code>


### そもそもnpmからわからない

#### nvmについて
Node.jsのバージョンを変更できる。

#### npm-check-updates (コマンド：ncu)
コマンドでアップデート情報を一括で確認可能。ncuコマンドで個別でパッケージの更新状況を確認できる。

<code>https://zenn.dev/antez/articles/a9d9d12178b7b2</code>

<hr>

## "23.10.25"

### 言葉を正しく使えないITエンジニアは三流エンジニア

結論：自分の使う言葉を担保できるだけの調査をしておこう。またjava => Java,javascript => JavaScriptなど正しい表記を意識する。

<code>https://s8a.jp/words-are-correctly</code>

### 私たちはどうして公式ドキュメントが読めないのか？

結論：公式ドキュメントを読む文化がないことや、公式ドキュメントを読む意味が感じられないの部分が自分に不足していると感じた。そのため一次情報を積極的に取得していくこと、読みに行く姿勢が必要だと感じた。

<code>https://qiita.com/hiraike32/items/f0a211cceb0ecc516b6c</code>

### async/await を完全に理解する



<code>https://zenn.dev/vatscy/articles/ba2263bdfadfeb805379</code>

<code>https://zenn.dev/nameless_sn/articles/mongodb_tutorial</code>
<code></code>
<code></code>
<hr>
<hr>
<hr>
<hr>