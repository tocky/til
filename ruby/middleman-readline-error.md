# Middleman を実行しようとしたときに readline 関連のエラー発生

久しぶりに [Middleman](https://middlemanapp.com/) を使おうとしたところ `middleman` コマンド実行時にエラーが出るようになってしまっていた。Ruby を使ったプロジェクトではよくあることだが、ネイティブライブラリを利用したコンパイルに失敗することに起因している。今回の場合には次のようなエラーが発生した。

```
$ middleman help
WARN: Unresolved specs during Gem::Specification.reset:
      json (>= 1.7.7, ~> 1.7)
      minitest (~> 5.1)
WARN: Clearing out unresolved specs.
Please report a bug if this causes problems.
    Sorry, you can't use byebug without Readline. To solve this, you need to
    rebuild Ruby with Readline support. If using Ubuntu, try `sudo apt-get
    install libreadline-dev` and then reinstall your Ruby.
/Users/tocky/.anyenv/envs/rbenv/versions/2.2.3/gemsets/middleman/gems/byebug-5.0.0/lib/byebug/history.rb:2:in `require': dlopen(/Users/tocky/.anyenv/envs/rbenv/versions/2.2.3/lib/ruby/2.2.0/x86_64-darwin15/readline.bundle, 9): Library not loaded: /usr/local/opt/readline/lib/libreadline.6.dylib (LoadError)
  Referenced from: /Users/tocky/.anyenv/envs/rbenv/versions/2.2.3/lib/ruby/2.2.0/x86_64-darwin15/readline.bundle
  Reason: image not found - /Users/tocky/.anyenv/envs/rbenv/versions/2.2.3/lib/ruby/2.2.0/x86_64-darwin15/readline.bundle
    from /Users/tocky/.anyenv/envs/rbenv/versions/2.2.3/gemsets/middleman/gems/byebug-5.0.0/lib/byebug/history.rb:2:in `<top (required)>'
    from /Users/tocky/.anyenv/envs/rbenv/versions/2.2.3/gemsets/middleman/gems/byebug-5.0.0/lib/byebug/interface.rb:1:in `require'
    from /Users/tocky/.anyenv/envs/rbenv/versions/2.2.3/gemsets/middleman/gems/byebug-5.0.0/lib/byebug/interface.rb:1:in `<top (required)>'
    from /Users/tocky/.anyenv/envs/rbenv/versions/2.2.3/gemsets/middleman/gems/byebug-5.0.0/lib/byebug/core.rb:5:in `require'
    from /Users/tocky/.anyenv/envs/rbenv/versions/2.2.3/gemsets/middleman/gems/byebug-5.0.0/lib/byebug/core.rb:5:in `<top (required)>'
    from /Users/tocky/.anyenv/envs/rbenv/versions/2.2.3/gemsets/middleman/gems/byebug-5.0.0/lib/byebug.rb:1:in `require'
    from /Users/tocky/.anyenv/envs/rbenv/versions/2.2.3/gemsets/middleman/gems/byebug-5.0.0/lib/byebug.rb:1:in `<top (required)>'
    from /Users/tocky/.anyenv/envs/rbenv/versions/2.2.3/gemsets/middleman/gems/pry-byebug-3.2.0/lib/byebug/processors/pry_processor.rb:1:in `require'
    from /Users/tocky/.anyenv/envs/rbenv/versions/2.2.3/gemsets/middleman/gems/pry-byebug-3.2.0/lib/byebug/processors/pry_processor.rb:1:in `<top (required)>'
    from /Users/tocky/.anyenv/envs/rbenv/versions/2.2.3/gemsets/middleman/gems/pry-byebug-3.2.0/lib/pry-byebug/pry_ext.rb:1:in `require'
    from /Users/tocky/.anyenv/envs/rbenv/versions/2.2.3/gemsets/middleman/gems/pry-byebug-3.2.0/lib/pry-byebug/pry_ext.rb:1:in `<top (required)>'
    from /Users/tocky/.anyenv/envs/rbenv/versions/2.2.3/gemsets/middleman/gems/pry-byebug-3.2.0/lib/pry-byebug/cli.rb:2:in `require'
    from /Users/tocky/.anyenv/envs/rbenv/versions/2.2.3/gemsets/middleman/gems/pry-byebug-3.2.0/lib/pry-byebug/cli.rb:2:in `<top (required)>'
    from /Users/tocky/.anyenv/envs/rbenv/versions/2.2.3/gemsets/middleman/gems/pry-0.10.1/lib/pry/plugins.rb:38:in `require'
    from /Users/tocky/.anyenv/envs/rbenv/versions/2.2.3/gemsets/middleman/gems/pry-0.10.1/lib/pry/plugins.rb:38:in `load_cli_options'
    from /Users/tocky/.anyenv/envs/rbenv/versions/2.2.3/gemsets/middleman/gems/pry-0.10.1/lib/pry/cli.rb:40:in `block in add_plugin_options'
    from /Users/tocky/.anyenv/envs/rbenv/versions/2.2.3/gemsets/middleman/gems/pry-0.10.1/lib/pry/cli.rb:39:in `each'
    from /Users/tocky/.anyenv/envs/rbenv/versions/2.2.3/gemsets/middleman/gems/pry-0.10.1/lib/pry/cli.rb:39:in `add_plugin_options'
    from /Users/tocky/.anyenv/envs/rbenv/versions/2.2.3/gemsets/middleman/gems/pry-0.10.1/lib/pry/cli.rb:107:in `<top (required)>'
    from /Users/tocky/.anyenv/envs/rbenv/versions/2.2.3/gemsets/middleman/gems/pry-0.10.1/lib/pry.rb:150:in `require'
    from /Users/tocky/.anyenv/envs/rbenv/versions/2.2.3/gemsets/middleman/gems/pry-0.10.1/lib/pry.rb:150:in `<top (required)>'
    from /Users/tocky/.anyenv/envs/rbenv/versions/2.2.3/lib/ruby/gems/2.2.0/gems/bundler-1.11.2/lib/bundler/runtime.rb:77:in `require'
    from /Users/tocky/.anyenv/envs/rbenv/versions/2.2.3/lib/ruby/gems/2.2.0/gems/bundler-1.11.2/lib/bundler/runtime.rb:77:in `block (2 levels) in require'
    from /Users/tocky/.anyenv/envs/rbenv/versions/2.2.3/lib/ruby/gems/2.2.0/gems/bundler-1.11.2/lib/bundler/runtime.rb:72:in `each'
    from /Users/tocky/.anyenv/envs/rbenv/versions/2.2.3/lib/ruby/gems/2.2.0/gems/bundler-1.11.2/lib/bundler/runtime.rb:72:in `block in require'
    from /Users/tocky/.anyenv/envs/rbenv/versions/2.2.3/lib/ruby/gems/2.2.0/gems/bundler-1.11.2/lib/bundler/runtime.rb:61:in `each'
    from /Users/tocky/.anyenv/envs/rbenv/versions/2.2.3/lib/ruby/gems/2.2.0/gems/bundler-1.11.2/lib/bundler/runtime.rb:61:in `require'
    from /Users/tocky/.anyenv/envs/rbenv/versions/2.2.3/lib/ruby/gems/2.2.0/gems/bundler-1.11.2/lib/bundler.rb:99:in `require'
    from /Users/tocky/.anyenv/envs/rbenv/versions/2.2.3/gemsets/middleman/gems/middleman-core-3.4.0/lib/middleman-core/load_paths.rb:37:in `setup_load_paths'
    from /Users/tocky/.anyenv/envs/rbenv/versions/2.2.3/gemsets/middleman/gems/middleman-core-3.4.0/bin/middleman:10:in `<top (required)>'
    from /Users/tocky/.anyenv/envs/rbenv/versions/2.2.3/gemsets/middleman/bin/middleman:23:in `load'
    from /Users/tocky/.anyenv/envs/rbenv/versions/2.2.3/gemsets/middleman/bin/middleman:23:in `<main>'
```

["Sorry, you can't use byebug without Readline" · Issue #289 · deivid-rodriguez/byebug](https://github.com/deivid-rodriguez/byebug/issues/289) によると `Gemfile` に `rb-readline` を追加すれば良いと書かれているので、そのとおりにした。またエラー冒頭の

```
WARN: Unresolved specs during Gem::Specification.reset:
      json (>= 1.7.7, ~> 1.7)
      minitest (~> 5.1)
```

を解決するために `bundle update` も行った。