# VRC Houdini勉強会 No.101

## 導入 
- コーディングエージェント以前の話としてvexとpythonをテキストエディタで書くためセットアップを紹介する
- テキストエディタのセットアップ
    - Houdini Expr Editor
        - vexを外部エディタで編集するためのアドオン
        - 使用方法：右クリックして`Expression/Edit in External Editor`を選択 
        - 現在はSideFXLabsに同梱されているので個別にインストールする必要はない
        - HoudiniExprEditorはテキストエディタで編集するためにtempファイルを作成している
            - デフォルトだとその際のファイルの作成場所がOSのtempフォルダになっている
            - $HIP/tempに作成するように修正した 
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
    - vexを快適に書くためのVScode拡張
        - Houdini Vex Help
            - F2でvex helpを開いてくれる
        - VEX or Houdini Vex
            - vex用のシンタックスハイライト
    - Python
        - 以下の設定でhouモジュールの補完ができる
        - 普通のpythonを書きたいタイミングもあるのでworkspaceごと設定している
        -`C:/PROGRA~1\\SIDEEF~1\\HOUDIN~1.522`は各自の`$HFS`を指定
        ```json:settings.json
            "python.autoComplete.extraPaths": [
                "C:/PROGRA~1\\SIDEEF~1\\HOUDIN~1.522\\houdini\\python3.11libs"
            ],
            "python.defaultInterpreterPath": "C:/PROGRA~1\\SIDEEF~1\\HOUDIN~1.522\\python311\\python.exe",
            "python.analysis.extraPaths": [
                "C:/PROGRA~1\\SIDEEF~1\\HOUDIN~1.522\\houdini\\python3.11libs"
            ]
        ```
-Reference
    - https://cgtoolbox.com/houdini-expression-editor/
    - https://qiita.com/gupon/items/9f93c678cde0a6fcd479
    - https://github.com/sideeffects/SideFXLabs/tree/Development/scripts/python/HoudiniExprEditor