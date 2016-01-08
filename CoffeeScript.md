# CoffeeScript

## CoffeeScript とは？
* JavaScript に変換可能な言語
* JavaScript に比べて…
	* 使いやすい
	* 書きやすい
	* 高機能
	* 最近人気
* hello.coffee -> hello.js といった感じでコンパイル


## CoffeeScript の導入
* Web上で試せるインタラクティブツール  
  http://coffeescript.org/
  
* node.jsの管理をhomebrewからnodebrewに変えて, npmをインストール  
  http://qiita.com/somtd@github/items/bd413e89d2db22ab795e
  
* 正しいcoffee-scriptの環境づくり vim  
  http://qiita.com/alpaca_taichou/items/fb442cfa78f91634cfaa


## 基本
* 行末までのコメントには `#` を使う
* 複数行のコメントは `###` で挟む
* varは不要
* 行末のセミコロンは不要
* ブロックはインデントで表現
* 丸括弧は曖昧性がない場合は省略可能

CoffeeScript:
	
	message = "Hello, world!"
	
	if message.length > 1
		alert message

JavaScript:

	var message;
	
	message = "Hello, world!";
	
	if (message.length > 1) alert(message);


## 文字列
* ダブルクオーテーション `"` で囲む
* 複数行文字列もOK
* ヒアドキュメントは `"""` で囲む

CoffeeScript:
	
	s = "Hello, world!"
	
	s = "Hello, 
	world!"
	
	s = """Hello,
	world!"""

JavaScript:

	var s;

	s = "Hello, world!";

	s = "Hello, world!";

	s = "Hello,\nworld!";

`#{var}` のように書くことで文字列中の変数展開ができる.

CoffeeScript:
	
	name = "questbeat"
	
	alert "Hello, #{name}!"

JavaScript:

	var name;

	name = "questbeat";

	alert("Hello, " + name + "!");


## 配列
CoffeeScript ではカンマではなく改行で区切ることができる.

CoffeeScript:

	m = [
		1, 5, 8
		2, 4, 2
	]

JavaScript:

	var m;

	m = [
		1, 5, 8,
		2, 4, 2,
	];

`[a..b]` のように書くと, 範囲 `a` から `b` の配列を作成できる.  
 また, `[a…b]` のように書くと `b` を含まなくなる.

CoffeeScript:

	m = [1..5]
	
	m = [1...5]

JavaScript:

	var m;

	m = [1, 2, 3, 4, 5];

	m = [1, 2, 3, 4];


## 連想配列
ブロック(波括弧)がインデントで表現できるので, 複雑な連想配列が簡単に書ける.

CoffeeScript:

	h =
		"questbeat":
			"sales": 200
			"cost": 80
		"kuebi":
			"sales": 250
			"cost": 40
			
JavaScript:

	var h;

	h = {
		"questbeat": {
			"sales": 200,
			"cost": 80
		},
		"kuebi": {
			"sales": 250,
			"cost": 40
		}
	};


## 条件分岐

### if
インデントでスッキリ書ける.

CoffeeScript:

	signal = "red"
	
	if signal == "red"
		alert "Stop!"
	else if signal == "green"
		alert "Go!"
	else
		alert "Caution!"

JavaScript:

	var signal;

	signal = "red";

	if (signal === "red") {
		alert("Stop!");
	} else if (signal === "green") {
		alert("Go!");
	} else {
		alert("Caution!");
	}

後置の `if` も可能.

CoffeeScript:

	x = 20
	
	alert "OK!" if x is 20

JavaScript:
	
	var x;

	x = 20;

	if (x === 20) {
		alert("OK!");
	}	

また, 比較演算子がいくつか追加されている.

* is (===)
* isnt (!==)
* not (!)
* and (&&)
* or (||)
* ? (存在チェック)

連結比較式も書ける.

CoffeeScript:
	
	x = 20
	
	if 10 < x < 30
		alert "OK!"

JavaScript:

	var x;

	x = 20;

	if ((10 < x && x < 30)) {
		alert("OK!");
	}


### switch
`case` ではなく `when`, `default` ではなく `else`.

CoffeeScript:

	signal = "red"
	
	switch signal
		when "red"
			alert "Stop!"
		when "green"
			alert "Go!"
		else
			alert "Caution!"
			
JavaScript:

	var signal;

	signal = "red";

	switch (signal) {
		case "red":
			alert("Stop!");
			break;
		case "green":
			alert("Go!");
			break;
		default:
 			alert("Caution!");
	}
	
	
## ループ

### for
CoffeeScript:
	
	for i in [0..3]
		alert i

JavaScript:

	var i, _i;

	for (i = _i = 0; _i <= 3; i = ++_i) {
		alert(i);
	}

### 配列のループ
`for-in` を使って列挙. 要素のインデックスも取得できる.

CoffeeScript:
	
	names = ["questbeat", "kuebi", "qb"]
	
	for name, index in names
		alert "Hello, #{name} (#{index})!"

JavaScript:

	var index, name, names, _i, _len;

	names = ["questbeat", "kuebi", "qb"];

	for (index = _i = 0, _len = names.length; _i < _len; index = ++_i) {
		name = names[index];
		alert("Hello, " + name + " (" + index + ")!");	}

### 連想配列のループ
`for-of` を使う. キーと値を取り出せる.

CoffeeScript:
	
	sales =
		"questbeat": 100
		"kuebi": 200
		"qb": 300
	
	for key, value of sales
		alert "#{key}: #{value}"

JavaScript:

	var key, sales, value;

	sales = {
		"questbeat": 100,
		"kuebi": 200,
		"qb": 300
	};

	for (key in sales) {
		value = sales[key];
		alert("" + key + ": " + value);
	}


## 関数

### 基本形
関数には `->` を使う.

CoffeeScript:

	hello = ->
		alert "Hello!"

JavaScript:

	function hello() {
		alert("Hello!");
	};

### 引数
引数アリの関数は `(args, …) ->` と書く.

CoffeeScript:

	hello = (name) ->
		alert "Hello, #(name)!"
		
	hello("questbeat")

JavaScript:

	var hello;
	
	hello = function(name) {
		return alert("Hello, " + name + "!");
	};
	
	hello("questbeat");

### 引数のデフォルト値
`label = default` のように書く.

CoffeeScript:

	hello = (name = "questbeat") ->
		alert "Hello, #(name)!"
		
	hello()

JavaScript:

	var hello;
	
	hello = function(name) {
		if (name == null) name = "questbeat";
		return alert("Hello, " + name + "!");
	};
	
	hello());
	
### 返り値のある関数
明示的に `return` する必要はなく, 最後に計算された値が自動的に返り値になる.

CoffeeScript:

	sum = (a, b) ->
		a + b
		
JavaScript:

	var sum;
	
	sum = function(a, b) {
		return a + b;
	};
