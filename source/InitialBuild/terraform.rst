=========================
Terraform実行環境構築
=========================

前提
========
- 以下の環境で構築を実施
	- WorkSpaces（Amazon Linux release 2 (Karoo)）
- 

事前準備
================
- AWSアカウントの作成
- terraformからAWSにアクセスするためのアクセスキー/シークレットアクセスキー
	1. AWSコンソールにログイン
	2. サービス「IAM」を選択
	3. 左ペインからユーザーを選択し、自分のユーザー名を選択
	4. 認証情報のタブから「アクセスキーの作成」をクリック
	5. 作成されたアクセスキーとシークレットアクセスキーをコピー

構築手順
================
AWS CLIインストール
---------------------

1. AWS CLI インストールファイルDL

.. code-block:: shell
	
	curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o ~/awscliv2.zip

2. インストールファイル展開

.. code-block:: shell
	
	unzip ~/awscliv2.zip

3. AWS CLI インストール

.. code-block:: shell
	
	sudo ~/aws/install

4. AWS CLIへの設定情報保存

.. code-block:: shell
	
	aws configure --profile {プロファイル名}

以下のように質問に答える。

.. code-block:: shell
	
	AWS Access Key ID [None]: {事前準備で用意したアクセスキー}
	AWS Secret Access Key [None]: {事前準備で用意したシークレットアクセスキー}
	Default region name [None]: ap-northeast-1
	Default output format [None]: json

Terraformインストール
---------------------
.. note::
	
	今回はtfenvというツールを使ってTerraformをインストールする
	
	tfenvとはTerraformを複数バージョンインストールして、切り替えて使用できるツール

1. Gitリポジトリーをclone

.. code-block:: shell
	
	git clone https://github.com/tfutils/tfenv.git ~/.tfenv

2. パスを通す

.. code-block:: shell
	
	vi ~/.bashrc
	
以下のように追記する

.. code-block:: shell
	 
	export PATH="$PATH:$HOME/.tfenv/bin"
	
設定を読み込む

.. code-block:: shell

	source .bashrc

3. tfenvでTerraformのインストール可能バージョンの確認

.. code-block:: shell

	tfenv list-remote

.. code-block:: shell

	1.5.0-alpha20230504
	1.5.0-alpha20230405
	1.4.6
	1.4.5
	1.4.4

今回は、最新かつ安定バージョンの「1.4.6」をインストールする

4. tfenv インストール

.. code-block:: shell
	
	tfenv install 1.4.6
	
5. 使用するTerraformバージョンの指定

.. code-block:: shell
	
	tfenv use 1.4.6

設定を確認する

.. code-block:: shell
	
	tfenv list

6. オートコンプリートの有効化

.. code-block:: shell
	
	terraform -install-autocomplete
	
git-secretsインストール
---------------------

.. note::
	git-secretsを利用する事により、AWSアクセスキー、AWSシークレットキーをgitリポジトリにコミットできないようにコミット直前にチェックできるようになる


1. Gitリポジトリーをclone

.. code-block:: shell
	
	git clone https://github.com/awslabs/git-secrets.git ~/.git-secrets
	
2. git-secrets インストール

.. code-block:: shell
	
	cd ~/.git-secrets/ && sudo make install
	
3. git-secrets をAWS用に設定

.. code-block:: shell
	
	git secrets --register-aws --global
	
4. Gitのカスタム

.. code-block:: shell
	
	git secrets --install ~/.git-templates/git-secrets
	git config --global init.templatedir '~/.git-templates/git-secrets'
	
5. 設定確認
以下のサイトを参考に、シークレットキーがcommitできないことを確認する

* `基本的な使い方 <https://qiita.com/jqtype/items/9196e047eddb53d07a91#%E5%9F%BA%E6%9C%AC%E7%9A%84%E3%81%AA%E4%BD%BF%E3%81%84%E6%96%B9>`_

参考
================
* `本番環境に対応したTerraform運用環境構築 <https://qiita.com/mttk030/items/fe11afddce39b9e5e60f>`_