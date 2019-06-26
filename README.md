# server_spec
# インストール＆セットアップ
- 参考文献
https://www.setouchino.cloud/blogs/38

## Rubyのインストール
```
yum install ruby
```

## Serverspecのインストール
```
gem install net-ssh -v 4.2.0
gem install serverspec rake highline
```
Serverspecインストール確認
```
gem list serverspec
```
作業ディレクトリ作成
```
mkdir serverspec_test
cd serverspec_test
```
sserverspec初期化
```
serverspec-init

Select OS type:

      1) UN*X
      2) Windows

    Select number: 1

    Select a backend type:

      1) SSH
      2) Exec (local)

    Select number: 2

    Vagrant instance y/n: n
    Input target host name: {HOSTNAME}
     + spec/
     + spec/{HOSTNAME}/
     + spec/{HOSTNAME}/sample_spec.rb
     + spec/spec_helper.rb
```
サンプルspecファイル作成
```
vim spec/localhost/sample_spec.rb
# 全部消して以下を追記
---
require 'spec_helper'

describe package('ruby'), :if => os[:family] == 'redhat' do
  it { should be_installed }
end
---
```
## Serverspec動作確認
```
rake spec
-->>
/usr/bin/ruby -I/usr/local/share/gems/gems/rspec-core-3.8.1/lib:/usr/local/share/gems/gems/rspec-support-3.8.2/lib /usr/local/share/gems/gems/rspec-core-3.8.1/exe/rspec --pattern spec/localhost/\*_spec.rb

Package "ruby"
  should be installed

Finished in 0.06187 seconds (files took 0.50206 seconds to load)
1 example, 0 failures

```
