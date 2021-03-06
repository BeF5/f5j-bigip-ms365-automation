MS365プロキシバイパス用URL/IPリスト更新自動化サンプルプログラム
===========================================================================================

BIG-IPをMicrosoft365のプロキシバイパスとして用いる際に、Microsoft社から配布されているEndpoint（URLやIPアドレス）のリストを自動で取得・更新するプログラムのサンプルコードです。

はじめに
--------------------------------
このページではMS365のエンドポイント(URLやIPアドレス)のリストを自動的に取得・更新するためのBIG-IP用のサンプルプログラムの提供およびその説明を致します。
BIG-IPでURLのリストを格納する場所として

* iRule DataGroup
* URLフィルタのカスタムカテゴリ

| がありますが、このページではDataGroupに格納するサンプルプログラムを掲載いたします。
| URLフィルタのカスタムカテゴリに格納するサンプルプログラムに関しましては

 | `Office 365 IP and URL Web Service Automation for BIG-IP`
 | https://github.com/brett-at-f5/f5-office365-ip-url-automation

をご参照ください。


コンテンツ
--------------------------------

o365update.pyの使い方 - 概要 `MANUAL1`__

.. _MANUAL1: ./latest/MANUAL1.rst

__ MANUAL1_

o365update.pyの使い方 - 詳細 `MANUAL2`__

.. _MANUAL2: ./latest/MANUAL2.rst

__ MANUAL2_

サンプルプログラム `o365update.py`__

.. _o365update.py: ./latest/o365update.py

__ o365update.py_


変更履歴
--------------------------------

v1.5 (2021.12.2)

* "category"フィールドの3種の値(Allow, Optimize, Default)のそれぞれに関して、"required"フィールドの値(true, false)ごとにURL/IPアドレスリストに取り込むか否かのオプションを追加

v1.4 (2021.10.22)

* Proxyサーバ経由でMicrosoft Web Serviceへ接続する機能を追加。認証無し、及びBasic認証をサポート

v1.3 (2021.7.2)

* "category"フィールドの値、"Allow"、"Optimize", "Default"のそれぞれに関して、URL/IPアドレスリストに取り込むか否かのオプションを追加
* MS側の仕様として"allowUrls"、"defaultUrls"というレコード、"serviceArea"レコードから"Yammer"という値が廃止されたため、当プログラムからも該当部分を削除

    - https://docs.microsoft.com/ja-jp/microsoft-365/enterprise/microsoft-365-ip-web-service

v1.2 (2019.7.26)

* 従来通りの全レコードを対象とするリスト作成に加え、Express Routeを通すもの、Express Routeを通さないものに関しても個別にURLリスト、IPv4アドレスリスト、IPv6アドレスリストを生成するオプションを追加。MSから配布されているJSONの"expressRoute"レコードの値に基づく。

当プログラムの仕様と理由に関するメモ
--------------------------------------
* BIG-IPにインストールされているPythonは2.xです。そのためこのサンプルプログラムもPython 2.xをベースに作成されています。
* BIG-IPにインストールされているthird-party softwareのバージョン詳細に関しては各TMOSバージョンのBIG-IP third-party software matrixをご参照ください

    - https://support.f5.com/csp/article/K48851448

* このサンプルプログラムはBIG-IPにデフォルトで含まれるPythonモジュールだけで動くように作成されています。PythonのrequestsモジュールはBIG-IPの仮想版には含まれていますが、ハードウェアアプライアンスには含まれていないため、本プログラムではrequestsモジュールは利用せず、httplibを用いています。
* JSONから条件を指定してレコードを抽出するにはjq等を用いるのが便利です。が、BIG-IPにはpyjqモジュールが含まれていないこと、またbashではjqコマンドが使えますが頻繁にpythonとbashのプレーンをまたいで実行することを避けるため、本プログラムではif文を多用して実装しています。
  
免責
^^^^^^^^^^^^^^^^^^
| 本資料は設計・構築を補助するための情報提供を目的としています。内容についてできる限り正確を期すよう努めてはおりますがいかなる明示または暗黙の保証も責任も負いかねます。本資料の情報は使用先の責任において使用されるべきものであることをあらかじめご了承ください。
| この文書に記載された製品の仕様ならびに動作に関しては各社ともにこれらを予告なく改変する場合があります。F5製品の各機能やコマンドに関する正式な情報に関してはAskF5（https://support.f5.com/）の対応するハードウェアプラットフォーム、ソフトウェアバージョンに即してご確認下さい。

