###
<h1>10月：積み上げ</h1>

###
"2023 10.01"
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

###
TypeScript intersection types

2つの型宣言がある場合、typeで型宣言をして、それらを結合する操作。結合する場合、type宣言して定義した型ともう一方の型をアンバサンド&で結合する。
ex. type User = Profile & Login

###
TypeScript union types
ある変数などに対して、型を二つ定義したいときに使用する。論理和の|を使用して定義する。
ex. let val : boolean | string;
    let array: (boolean | string)[];

###
TypeScript literal types
ある変数に代入できる者を限定することが可能。（文字列、数字でも可能）
ex. let company : "Facebook" | "Twitter" | "Apple" ;
    company = "Facebook";
    company = "amazon"は代入不可

###
TypeScript typeof 
ある宣言済みの変数などに定義された型を別の変数の型に継承するやり方。宣言済みの変数の型以外の型のものを代入するとエラーになる。宣言済みかどうかは型推論できているかどうか。オブジェクト形式の型も継承可能。
ex. let msg: string = "Hello"
    let talk: typeof msg;

###
TypeScript keyof 
キー情報を型で定義して、そのキーをユニオン型で継承して使用するキーの部分の型宣言。
ex. type Keys = { primary: string, secondary: string}
    let keys :keyof : Keys 
    key = primary 


###
keyof + typeof
ex. const Sport = {
    soccer: "soccer",
    baseball: "baseball",
}

let keySports: keyof typeof Sport
型とキー情報を継承して使用することが可能。

###
TypeScript enum
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

###
useReducer

分からない部分：useStateとuseReducerの違い。

理解したこと：処理条件を複数設置することが可能になる。dispatch関数を実行することで、useReducerの第一引数の処理が実行される。

ref
https://qiita.com/hibi_toshi/items/ad5b79f20547d5eb8d05?utm_campaign=post_article&utm_medium=twitter&utm_source=twitter_share&s=09
https://reffect.co.jp/react/react-hook-reducer-understanding/






<hr>
<hr>
<hr>
<hr>
