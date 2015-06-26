実行方法

::

   ansible-playbook -i inventory/production common_init.yml jboss.yml



ポイント
------------

playbook
`````````

- `common_init` などの、共通設定を行うplaybookを設定しておくと楽
- ansible-playbookコマンドは複数のplaybook.ymlを引数に与えてもそれぞれ実行してくれる
  - sshを張り直すので、remote_userが異なっても平気
- user追加はノードごとにいろいろ違う場合があるので変数に切り出しておく
  - dict形式にして、with_dictで使うようにすればいろいろな情報をuserに付け加えられる
  

変数
````````````

ansibleは変数の扱いを慎重に行わないと破綻していきます。

- roles内での変数は "jboss_http_port" などのように、role名を先頭につける
- roles/defaults/main.ymlは初期設定変数で、確実に上書きできる
- group_varsディレクトリ以下にファイルを置くと、自動的にそのグループの変数を読み込んでくれる
- varsディレクトリ以下にいろいろな変数設定を置く
  - vars_filesで複数のファイルを読み込める
  - ansible-vaultもこの単位で切り出せばいい


   
