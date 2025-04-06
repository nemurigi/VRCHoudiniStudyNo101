# VRC Houdini勉強会 No.101 
- コーディングエージェント以前の話としてvexとpythonをテキストエディタで書くためセットアップを紹介する
- [Houdini Expr Editor](https://cgtoolbox.com/houdini-expression-editor/)
    - vexやpythonを外部エディタで編集するためのアドオン
    - 使用方法：Expressionを右クリックして`Expression/Edit in External Editor`を選択 
    - 現在はSideFXLabsに同梱されているので個別にインストールする必要はない
    - 自分は少しだけ改造している
        - デフォルトだとtempファイル作成時にOSのtempフォルダに配置する
        - それを`$HIP/temp`に配置するように改造
        ```python:ParmWatcher.py
        # TEMP_FOLDER = os.environ.get("EXTERNAL_EDITOR_TEMP_PATH",
        #                              tempfile.gettempdir())

        # tempファイルの保存先を$HIP/tempに変更
        TEMP_FOLDER = (
            os.path.join(hou.expandString("$HIP"), "temp")
            if hou.getenv("HIP")
            else os.environ.get("EXTERNAL_EDITOR_TEMP_PATH", tempfile.gettempdir())
        )
        ```
- VEX
    - おすすめVScode拡張
        - [Houdini Vex Help](https://marketplace.visualstudio.com/items?itemName=cgtoolbox-guillaume-jobst.houdinivexhelp)
            - F2でvex helpを開いてくれる
        - [VEX](https://marketplace.visualstudio.com/items?itemName=melmass.vex) or [Houdini Vex](https://marketplace.visualstudio.com/items?itemName=supernova-explosion.houdini-vex)
            - vex用のシンタックスハイライト
    - `$HIP/vex/include`に.vflを配置するとwrangleから読み込める
        - ref [VEXで外部vflの読み込み](https://qiita.com/gupon/items/9f93c678cde0a6fcd479)
- Python
    - houモジュールの補完用の`settings.json`の設定
        - 普通のpythonを書きたいタイミングもあるのでworkspaceごと設定している
        - `C:/PROGRA~1\\SIDEEF~1\\HOUDIN~1.522`は各自の`$HFS`を指定
    ```json:settings.json
        "python.autoComplete.extraPaths": [
            "C:/PROGRA~1\\SIDEEF~1\\HOUDIN~1.522\\houdini\\python3.11libs"
        ],
        "python.defaultInterpreterPath": "C:/PROGRA~1\\SIDEEF~1\\HOUDIN~1.522\\python311\\python.exe",
        "python.analysis.extraPaths": [
            "C:/PROGRA~1\\SIDEEF~1\\HOUDIN~1.522\\houdini\\python3.11libs"
        ]
    ```