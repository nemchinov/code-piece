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