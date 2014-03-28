---
title: Middleman
---

# Middlemanとは？

`Middleman` はRuby製(Sinatra)の静的 Web サイトを作成するためのコマンドラインツールで静的サイトジェネレータ（Static Site Generator）とか呼ばれてます。

### [Jekell](http://jekyllrb.com/)
一番知られているジェネレーター。これとJekellの機能を拡張する[Octopress](http://octopress.org/)の組み合わせで使用する人が多い。

### [Hyde](http://ringce.com/hyde)
名前の通りJekellを意識して作られたPython製のジェネレーターでD​​jangoのテンプレートを利用できるようです。
ただ、日本語のドキュメントが少ないのであまり国内では使用してる人はいないみたい。

### [roots](http://roots.cx/)
node.js製の多機能ジェネレーター。グローバル変数やビューヘルパーなども使えるとあります。
Jade、Stylus、CoffeeScriptをデフォルトで使用できるようになっており、またファイルの変更があれば、自動的にコンパイルする機能もあります。HerokuやGithub Pagesにデプロイする機能もあります。

### [Sculpin](https://sculpin.io/)
PHP製のジェネレーター。Jekellに足りない部分を補足する形で作られたらしい。Octopressに近い使用感らしい。

## Middlemanで出来ること

+ ヘッダー、フッターなど共通部分を共有させることが出来る。　
+ HTML内でRubyの文法が使えるHTMLテンプレートエンジンのERBが使える。
+ Haml、Slim、Sass、Less、Stylus、CoffeeScriptなどのCSS拡張メタ言語やAltJSが使える。
+ 開発中は開発コードとプロダクションコードを分離出来る。
+ LiveReloadで自動コンパイル。
+ 便利なTemplate Helpersが使える。
+ Asset PipelineでJavascriptやCSSの依存ファイルを管理。
+ JavascriptやCSSをminify、gzipなど最適化。

などなど

## インストール

`Middleman` は `RubyGems` を使ってインストールできます。


	gem install middleman



簡単！



	middleman --help

	middleman build [options]           # Builds the static site for deployment
	middleman console [options]         # Start an interactive console in the context of your Middleman application
	middleman extension NAME [options]  # Create Middleman extension scaffold NAME
	middleman init NAME [options]       # Create new project NAME
	middleman server [options]          # Start the preview server
	middleman upgrade                   # Upgrade installed bundle
	middleman version                   # Show version


## プロジェクトフォルダを作る

コマンドで新しいサイト用のフォルダを指定することで, 指定フォルダの中にプロジェクトのスケルトンを作ります (場合によってはフォルダも)。


	middleman init my_new_project

以下のスケルトンが作成されます。

	my_new_project/
	├── Gemfile
	├── Gemfile.lock
	├── config.rb
	└── source
	    ├── images
	    ├── index.html.erb
	    ├── javascripts
	    ├── layouts
	    └── stylesheets

**Gemfile** - 
	Bundler の Gemfile を使って gem の依存関係の管理。これにより プロジェクトを を特定のリリースシリーズに固定出来る。

**Gemfile.lock** - 
	インストール済のGemと依存関係にある Gem を記述。

**config.rb** - 
	設定ファイル。

**source** - 
	実際に開発していくファイルが格納されていて、ここがビルド対象となります。


## プロジェクトテンプレート

標準のスケルトン以外に `HTML5 Boilerplate`, `SMACSS`, や `Mobile Boilerplate` ベースのオプションテンプレートが付いています。

	middleman init my_new_boilerplate_project --template=html5

	middleman init my_new_mobile_project --template=smacss

	middleman init my_new_mobile_project --template=mobile


それ以外にも [コミュニティで開発されたテンプレート](http://directory.middlemanapp.com/#/templates/all) も使うことが出来る。


## 開発手順

Middlemanは開発コードとプロダクションコード分離されています、またローカルの Web サーバを起動させ動的に表示
するので都度 build する必要も無い。

開発時は以下のようにプレビューサーバを起動します。

	bundle exec middleman server

このコマンドで Web サーバを起動 `http://localhost:4567/`

## 静的サイトのエクスポート

編集したファイルをサーバー側に送りたい場合は静的ページを出力します。

	bundle exec middleman build


# テンプレート

Middlemanでは基本はテンプレート言語 ERbを使用し Template , layout , partial　という構成で構築されます。

# テンプレートヘルパ

テンプレートヘルパはよくある HTML の作業を簡単にするため, 動的テンプレートの中で使用できるメソッドで Rails のビューヘルパを利用したことのある人にはお馴染みのものです。（使ったこと無いので御馴染みではなかったですが...）

+ リンクヘルパ
+ 出力ヘルパ
+ タグヘルパ
+ アセットヘルパ
+ Form ヘルパ
+ フォーマットヘルパ
+ ダミーテキスト & Placehold.it ヘルパ


## リンクヘルパ

リンクタグを作るために `link_to` メソッドを提供しています基本的な使い方は `link_to` がリンク名とリンク URL を引数に取ります

	<%= link_to '私のサイト', 'http://mysite.com' %>

ブロックをとることも出来る

	<% link_to 'http://mysite.com' do %>
	  <%= image_tag 'mylogo.png' %>
	<% end %>


