# To-Do リスト管理ツール (CLI)
このプロジェクトは、Pythonのコマンドラインインターフェース（CLI）で動作するシンプルなTo-Doリスト管理ツールです。タスクの追加、優先度付け、表示、および完了（削除）の機能を提供します。

## 🚀 機能一覧
* **タスクの追加**: タスク名と優先度（高 / 中 / 低）を指定してタスクを追加できます。
* **優先度ソート**: タスク一覧表示時、自動的に優先度順（高 → 中 → 低）に並び替えて表示します。
* **データ永続化**: 終了時または実行中にタスクリストを todo_data.json ファイルに自動保存・読み込みます。
* **安全な削除**: ソートされて表示された番号で、インデックスのズレを気にせず正確にタスクを削除できます。

## 🛠️ 技術的なポイント
* データ構造の採用: タスクはシンプルな文字列ではなく、キーを持つ辞書として管理されます。これにより、複数の属性（タスク名と優先度）を一つの要素として扱えます。
* 優先度ソートのロジック: タスクのソートには、Pythonの sorted() 関数と、カスタムの key 関数を使用しています。
  1. priority_map = {"高": 1, "中": 2, "低": 3} を定義し、文字列を数値にマッピング。
  2. get_priority_value 関数が、タスクの優先度をこの数値に変換し、sorted() 関数にソート基準を提供します。
* 削除処理の安全性: 一覧表示時と内部データ（todo_list）のインデックスのズレを防ぐため、以下の手法を採用しています。
  1. view_tasks がソート後のリスト（sorted_list）を返します。
  2. complete_task は、その sorted_list とユーザーが入力した番号を使って、削除対象のタスク辞書そのものを特定します。
  3. todo_list.remove(task_to_delete) を使用し、インデックスではなく辞書の内容を比較して元のリストからタスクを削除します。これにより、データの一貫性を保ちます。

## 💻 実行方法
1. 上記の todo_app.py ファイルを保存します。
2. ターミナルまたはコマンドプロンプトで以下のコマンドを実行します。
   python todo_app.py


----- **English Version** -----

## To-Do List Management Tool (CLI)

This project is a simple To-Do list management tool implemented in Python, designed to be run via the Command Line Interface (CLI). It provides core functionalities for adding, prioritizing, viewing, and completing (deleting) tasks.

### 🚀 Key Features
* **Task Addition**: Users can add a task by specifying the task name and its priority (High / Medium / Low).
* **Priority Sorting**: The task list is automatically sorted and displayed in **priority order** (High -> Medium -> Low).
* **Data Persistence**: The task list is automatically saved to and loaded from the `todo_data.json` file upon exit or launch.
* **Safe Deletion**: Tasks can be reliably deleted using the number displayed in the sorted list, eliminating index mismatch issues.

### 🛠️ Technical Deep Dive
* **Data Structure**: Tasks are managed not as simple strings, but as **Dictionaries** with specific keys. This allows for handling multiple attributes (task name and priority) as a single element.
* **Priority Sorting Logic**: The sorting mechanism utilizes Python's built-in `sorted()` function combined with a custom `key` function.
    1. A mapping dictionary, `priority_map = {"高": 1, "中": 2, "低": 3}`, is defined to translate priority strings into sortable numerical values.
    2. The `get_priority_value` function converts the task's priority string into this numerical value, providing the sort criterion for the `sorted()` function.
* **Safe Deletion Process**: To prevent index discrepancies between the displayed (sorted) list and the internal data list (`todo_list`), the following method is employed:
    1. `view_tasks` returns the sorted list (`sorted_list`).
    2. `complete_task` uses the `sorted_list` and the user-inputted number to identify the **exact task dictionary** intended for deletion.
    3. `todo_list.remove(task_to_delete)` is then used. This method compares the **content** (the entire dictionary) rather than the index, ensuring that the correct task is removed from the original internal list, maintaining data integrity.

### 💻 How to Run
1. Save the `todo_app.py` file mentioned above.
2. Execute the following command in your terminal or command prompt:
   python todo_app.py
