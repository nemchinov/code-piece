1. Склейка коммитов 
    ```
    git rebase -i HEAD~<кол-во коммитов назад для склейки>
    ```
2. Отмена коммита без потери изменений
    ```
    git reset --soft HEAD^
    ```
3. Добавление правок в существующий коммит
    ```
    git comit --amend --no-edit
    ```
4. Stash
    ```
    git stash
    git stash list
    git stash apply [ключ засташенного кода]
    ```
5. gitignore:  
    * `*.txt` - ignores all .txt files JUST in the current folder
    * `**.txt` - ignores all .txt recursive from the current folder
    * `**/*.txt` - ignores all .txt in subdirectories recursive from the current folder (does not include the current folder)
    * `**/test` - ignores all files and folder with name test in subdirectories
6. GitHub Pages можно включить в настройках репозитория