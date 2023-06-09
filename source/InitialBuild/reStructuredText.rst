========================================
Sphinxでの文章の書き方(reStructuredText)
========================================

ここでは、自分がよく使う書き方を集めてみました。


.. _TOP:

セクション
==========

セクション名となる文字列の下に、-や=で線を引きます。これでセクションを作ることができます。
セクションは全部で６レベル分作ることができ、出現した順番にレベル分けされます。
セクション名に使用できる記号はたくさんありますが、見やすさから::

    = - ` : . ' " ~ ^ _ * + #

これらが推奨されているようです。

::

    =====================
    セクション(レベル１)
    =====================

    レベル２
    ========

    レベル３
    --------

    レベル４
    ^^^^^^^^

**出力例**

レベル２
========

レベル３
--------

レベル４
^^^^^^^^

出力例終わり



強調
====

======== =========== ============ ===================
         使用例      書き方       HTMLタグ
======== =========== ============ ===================
強調     *文字列*    \*で囲む     <em>
強い強調 **文字列**  \*\*で囲む   <strong>
コード   ``文字列``  \`\`で囲む   <span class="pre">
======== =========== ============ ===================



引用
====
前の段落より１段インデントが深い段落は引用になります。::

    以下は引用文です。
    
        こんにちは
        こんにちは
        こんにちは

    ここは引用文ではありません。

.. 出力例**

以下は引用文です。

    こんにちは
    こんにちは
    こんにちは

ここは引用文ではありません。
   

改行をそのまま表示したい場合には、ラインブロックを使います。

.. code-block:: rst

    | これらの行は、
    | ソースファイルと同じように
    | 改行されます。


| これらの行は、
| ソースファイルと同じように
| 改行されます。



番号なしリスト
==============
\*、+、-を使って項目を並べるとリストになります。

::

    * 項目1
    * 項目2
    * 項目3

    + 項目1
    + 項目2
    - 項目3


**出力例**

* 項目1
* 項目2
* 項目3

+ 項目1
+ 項目2

- 項目1
- 項目2



番号付きリスト
===============

.. code-block:: rst

    1. 項目1
    2. 項目2
    3. 項目3

    #. 項目1
    #. 項目2
    #. 項目3


1. 項目1
2. 項目2
3. 項目3

#. 項目1
#. 項目2
#. 項目3


コードブロック
===============
\:\:のあと１行開けてから１段インデントして書く。

::

    ふつうの文章::

        コードブロック

    ふつうの文章


またはcode-blockディレクティブを使います。::

    .. code-block:: python

        import sys

        print sys.path

code-blockディレクティブではどのシンタックスハイライトを使うかを指定することができます。



ラベルと参照
============
文章中で他の文章にリンクを張りたい場合があると思います。

その場合、 **ラベル** をつけておき、そこに対してrefでリンクを作ることができます。

.. code-block:: rst

    .. _label:

    タイトル
    =========
    文章

    :ref:`label` を参照


以下はサンプルです。

.. _label:

タイトル
--------
文章

:ref:`label` を参照


リンク
========
次のようにリンクを書くことができます。::

    資料
    ====

    * http://sphinx-doc.org/
    * `github <https://github.com>`_
    * Sphinx-users.jp_

    .. _Sphinx-users.jp: http://sphinx-users.jp/


1. 普通にURLを書くと自動でリンクになる。
2. 文字列_ または `スペースを 含む文字列`_ と書いておいて、
   あとから \.\. \_`スペースを 含む文字列`: URL とするとリンクになる。
3. `文字列 <URL>`_ とするとリンクになる。

.. _`スペースを 含む文字列`: http://localhost/

どの方法が良いというわけはありません。

3の方法は同じ文言を同じリンクにしたい場合には
有効ですが、文字列と実際のリンクURLが離れてしまう欠点もあります。

逆に、2の方法で、同じ文字列に対して2回書いてしまうと、ビルド時に警告がでます。


ダウンロード用のリンク
======================
以下のように書きます。::

    :download:`このファイル <03.rst>`


「 :download:`このファイル <./03.rst>` 」のようにリンクが出来ます。

また、リンクだけでなく、出力ディレクトリに_downloadsディレクトリが作成され、
その中にdownloadで指定したファイルが格納されます。



画像
====

.. code-block:: rst

    .. image::


.. code-block:: rst

    .. figure:: 



テーブル
========

テーブル1
----------

.. code-block:: rst

    ======= ====== ======
    col1    col2   col3
    ======= ====== ======
    row1    a      b
    row2    a      b
    row3    a      b
    ======= ====== ======


======= ====== ======
col1    col2   col3
======= ====== ======
row1    a      b
row2    a      b
row3    a      b
======= ====== ======


テーブル2
----------

.. code-block:: rst

    +------------------------+------------+----------+----------+
    | Header row, column 1   | Header 2   | Header 3 | Header 4 |
    | (header rows optional) |            |          |          |
    +========================+============+==========+==========+
    | body row 1, column 1   | column 2   | column 3 | column 4 |
    +------------------------+------------+----------+----------+
    | body row 2             | ...        | ...      |          |
    +------------------------+------------+----------+----------+


+------------------------+------------+----------+----------+
| Header row, column 1   | Header 2   | Header 3 | Header 4 |
| (header rows optional) |            |          |          |
+========================+============+==========+==========+
| body row 1, column 1   | column 2   | column 3 | column 4 |
+------------------------+------------+----------+----------+
| body row 2             | ...        | ...      |          |
+------------------------+------------+----------+----------+


csv-table
----------

.. code-block:: rst

    .. csv-table:: Frozen Delights!
        :header: "Treat", "Quantity", "Description"
        :widths: 15, 10, 30

        "Albatross", 2.99, "On a stick!"
        "Crunchy Frog", 1.49, "If we took the bones out, it wouldn't be
        crunchy, now would it?"
        "Gannet Ripple", 1.99, "On a stick!"


.. csv-table:: Frozen Delights!
   :header: "Treat", "Quantity", "Description"
   :widths: 15, 10, 30

   "Albatross", 2.99, "On a stick!"
   "Crunchy Frog", 1.49, "If we took the bones out, it wouldn't be
   crunchy, now would it?"
   "Gannet Ripple", 1.99, "On a stick!"


list-table
------------

.. code-block:: rst

    .. list-table:: Frozen Delights!
        :widths: 15 10 30
        :header-rows: 1

        * - Treat
            - Quantity
            - Description
        * - Albatross
            - 2.99
            - On a stick!
        * - Crunchy Frog
            - 1.49
            - If we took the bones out, it wouldn't be
            crunchy, now would it?
        * - Gannet Ripple
            - 1.99
            - On a stick!

.. list-table:: Frozen Delights!
   :widths: 15 10 30
   :header-rows: 1

   * - Treat
     - Quantity
     - Description
   * - Albatross
     - 2.99
     - On a stick!
   * - Crunchy Frog
     - 1.49
     - If we took the bones out, it wouldn't be
       crunchy, now would it?
   * - Gannet Ripple
     - 1.99
     - On a stick!

     
注釈
====

ノート

.. note::
    
    これは注釈です！

.. code-block:: rst

    .. note::

        これは注釈です！

警告

.. warning::
    
    これは警告です！

.. code-block:: rst

    .. warning::

        これは警告です！


索引
====
indexディレクティブを設定することで、索引を作ることができます。

.. index:: Python


.. index::
    pair: Python; Sphinx


.. code-block:: rst
    
    .. index:: Python
    
    .. index::
        pair: Python; Sphinx
    

* :ref:`genindex`


他のファイルのインクルード
==========================
ファイルをreStructuredTextとして取り込みたい場合には includeを使用します。

.. code-block:: rst

    .. include:: include.rst


.. include:: include.rst


ファイルを引用として取り込みたい場合には、literalincludeを使用します。

.. code-block:: rst

    .. literalinclude:: include.rst
        :language: rst
        :linenos:


.. literalinclude:: include.rst
    :language: rst
    :linenos:


Todo
==========================

参考
====
* `reSTおよびSphinxで文章を書く際のtips - そこはかとなく書くよ。 <http://d.hatena.ne.jp/rudi/20110127/1296116839>`_
* `Sphinxマークアップ集 — Sphinx v1.0 (hg) documentation <http://sphinx.shibu.jp/markup/>`_
* `[翻訳] reStructuredText ディレクティブ - 清水川Web <http://www.freia.jp/taka/docs/misc/restructuredtext-directives.html>`_