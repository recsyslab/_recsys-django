# マイグレーションの実行

これで、データベースの設定ができました。`manage.py`があるディレクトリにいることを確認したうえで、以下のコマンドを実行してください。ただし、【ユーザ名】と【パスワード】には、それぞれデータベースに接続するユーザ名とパスワードを入力してください。

```bash
$ export DB_USER=【ユーザ名】
$ export DB_PASSWORD=【パスワード】
$ python manage.py migrate
```

すると、

```bash
Operations to perform:
  Apply all migrations: admin, auth, contenttypes, sessions
Running migrations:
  Applying contenttypes.0001_initial... OK
  Applying auth.0001_initial... OK
  Applying admin.0001_initial... OK
  Applying admin.0002_logentry_remove_auto_add... OK
  Applying admin.0003_logentry_add_action_flag_choices... OK
  Applying contenttypes.0002_remove_content_type_name... OK
  Applying auth.0002_alter_permission_name_max_length... OK
  Applying auth.0003_alter_user_email_max_length... OK
  Applying auth.0004_alter_user_username_opts... OK
  Applying auth.0005_alter_user_last_login_null... OK
  Applying auth.0006_require_contenttypes_0002... OK
  Applying auth.0007_alter_validators_add_error_messages... OK
  Applying auth.0008_alter_user_username_max_length... OK
  Applying auth.0009_alter_user_last_name_max_length... OK
  Applying auth.0010_alter_group_name_max_length... OK
  Applying auth.0011_update_proxy_permissions... OK
  Applying auth.0012_alter_user_first_name_max_length... OK
  Applying sessions.0001_initial... OK
```

というメッセージが出力されました。

PostgreSQL上で下記のコマンドを実行してください。

```pgsql
webgame=# \dt
```

すると、

```pgsql
                     リレーション一覧
 スキーマ |            名前            |    型    | 所有者 
----------+----------------------------+----------+--------
 public   | auth_group                 | テーブル | 【ユーザ名】
 public   | auth_group_permissions     | テーブル | 【ユーザ名】
 public   | auth_permission            | テーブル | 【ユーザ名】
 public   | auth_user                  | テーブル | 【ユーザ名】
 public   | auth_user_groups           | テーブル | 【ユーザ名】
 public   | auth_user_user_permissions | テーブル | 【ユーザ名】
 public   | django_admin_log           | テーブル | 【ユーザ名】
 public   | django_content_type        | テーブル | 【ユーザ名】
 public   | django_migrations          | テーブル | 【ユーザ名】
 public   | django_session             | テーブル | 【ユーザ名】
(10 行)
```

このように自動的にテーブルが作成されていることが確認できました。

先に入力したコマンドはマイグレーションを実行するためのコマンドです。マイグレーションを実行することで、設定ファイルおよびモデルの定義から、自動的にテーブルを作成したり、変更したりしてくれます。現時点では、モデルの定義を行っていませんが、それでも既にこれだけのテーブルが自動作成されました。

マイグレーションの詳細については、文献[1]を参照してください。

#### 参考
1. 現場で使える Django の教科書《基礎編》 # 第11章 データベースのマイグレーション (Model)