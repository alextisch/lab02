### Часть 1

1. Создайте пустой репозиторий на сервисе github.com (или gitlab.com, или bitbucket.com).
```
done
```
2. Выполните инструкцию по созданию первого коммита на странице репозитория, созданного на предыдещем шаге.
```
done
```
3. Создайте файл `hello_world.cpp` в локальной копии репозитория (который должен был появиться на шаге 2). Реализуйте программу **Hello world** на языке C++ используя плохой стиль кода. Например, после заголовочных файлов вставьте строку `using namespace std;`.
```sh
$ cat > hello_world.cpp <<EOF
heredoc> #include <iostream>
heredoc> 
heredoc> using namespace std;
heredoc> 
heredoc> int main() {
heredoc>        cout << "Hello, World!" << endl;
heredoc>        return 0;
heredoc> }
heredoc> EOF
```
4. Добавьте этот файл в локальную копию репозитория.
```sh
$ git status             
On branch main
Your branch is up to date with 'origin/main'.

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        hello_world.cpp

nothing added to commit but untracked files present (use "git add" to track)
$ git add hello_world.cpp

```
5. Закоммитьте изменения с *осмысленным* сообщением.
```sh
$ git commit -m "added hello_world.cpp with bad code style"
[main f2b3840] added hello_world.cpp with bad code style
 1 file changed, 8 insertions(+)
 create mode 100644 hello_world.cpp
```
6. Изменитьте исходный код так, чтобы программа через стандартный поток ввода запрашивалось имя пользователя. А в стандартный поток вывода печаталось сообщение `Hello world from @name`, где `@name` имя пользователя.
```sh
$ cat > hello_world.cpp <<EOF                
heredoc> #include <iostream>
heredoc> #include <string>
heredoc> 
heredoc> using namespace std;
heredoc> 
heredoc> int main() {
heredoc>        string name;
heredoc>        cout << "Enter your name, please: ";
heredoc>        cin >> name;
heredoc>        cout << "Hello world from " << name << "!" << endl;
heredoc>        return 0;
heredoc> }
heredoc> EOF
```
7. Закоммитьте новую версию программы. Почему не надо добавлять файл повторно `git add`?
```sh
$ git commit -m "updated hello_world.cpp with bad code style"
[main 1a28873] updated hello_world.cpp with bad code style
 1 file changed, 5 insertions(+), 1 deletion(-)
```
8. Запуште изменения в удалёный репозиторий.
```sh
$ git push -u origin main                                      
Enumerating objects: 7, done.
Counting objects: 100% (7/7), done.
Delta compression using up to 16 threads
Compressing objects: 100% (6/6), done.
Writing objects: 100% (6/6), 808 bytes | 808.00 KiB/s, done.
Total 6 (delta 1), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (1/1), done.
   1d94cb7..1a28873  main -> main
branch 'main' set up to track 'origin/main'.
```
9. Проверьте, что история коммитов доступна в удалёный репозитории.
```
done
```
### Часть 2

**Note:** *Работать продолжайте с теми же репоззиториями, что и в первой части задания.*
1. В локальной копии репозитория создайте локальную ветку `patch1`.
```sh
$ git checkout -b patch1
Switched to a new branch 'patch1'
```
2. Внесите изменения в ветке `patch1` по исправлению кода и избавления от `using namespace std;`.
```sh
$ cat > hello_world.cpp <<EOF
#include <iostream>
#include <string>

int main() {
        std::string name;
        std::cout << "Enter your name, please: ";
        std::cin >> name;
        std::cout << "Hello world from " << name << "!" << std::endl;
        return 0;
}  
EOF
```
3. **commit**, **push** локальную ветку в удалённый репозиторий.
```sh
$ git status            
On branch patch1
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   hello_world.cpp

no changes added to commit (use "git add" and/or "git commit -a")
$ git commit -a -m "updated hello_world.cpp without bad code style"
[patch1 24e261c] updated hello_world.cpp without bad code style
 1 file changed, 4 insertions(+), 6 deletions(-)
$ git push -u origin patch1 
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 16 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 417 bytes | 417.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
remote: 
remote: Create a pull request for 'patch1' on GitHub by visiting:

 * [new branch]      patch1 -> patch1
branch 'patch1' set up to track 'origin/patch1'.
```
4. Проверьте, что ветка `patch1` доступна в удалёный репозитории.
```
done
```
5. Создайте pull-request `patch1 -> master`.
```
"able to merge" -> "create pull request" -> "No conflicts with base branch" -> "Merge pull request #1 from alextisch/patch1" -> "Confirm merge"
```
6. В локальной копии в ветке `patch1` добавьте в исходный код комментарии.
```sh
$ cat > hello_world.cpp <<EOF
#include <iostream>
#include <string>

int main() {
        std::string name;
        std::cout << "Enter your name, please: "; // user enter its name
        std::cin >> name;
        std::cout << "Hello world from " << name << "!" << std::endl;
        return 0;
}  
EOF 
```
7. **commit**, **push**.
```sh
$ git commit -a -m "updated hello_world.cpp with comment"       
[patch1 b9baf3b] updated hello_world.cpp with comment
 1 file changed, 1 insertion(+), 1 deletion(-)
$ git push -u origin patch1                              
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 16 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 329 bytes | 329.00 KiB/s, done.
Total 3 (delta 2), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
   24e261c..b9baf3b  patch1 -> patch1
branch 'patch1' set up to track 'origin/patch1'.
```
8. Проверьте, что новые изменения есть в созданном на **шаге 5** pull-request
```
"Able to merge" -> "Create pull request"
done
```
9. В удалённый репозитории выполните  слияние PR `patch1 -> master` и удалите ветку `patch1` в удаленном репозитории.
```
"Create pull request" -> "Merge pull request" -> "Confirm merge"
patch1 deleted
```
10. Локально выполните **pull**.
```sh
$ git checkout main  
Switched to branch 'main'
Your branch is up to date with 'origin/main'.
$ git pull origin main  
remote: Enumerating objects: 2, done.
remote: Counting objects: 100% (2/2), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 2 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
Unpacking objects: 100% (2/2), 1.79 KiB | 1.79 MiB/s, done.
 * branch            main       -> FETCH_HEAD
   1a28873..2486fd5  main       -> origin/main
Updating 1a28873..2486fd5
Fast-forward
 hello_world.cpp | 10 ++++------
 1 file changed, 4 insertions(+), 6 deletions(-)
```
11. С помощью команды **git log** просмотрите историю в локальной версии ветки `master`.
```sh
$ git log             
commit 2486fd5b2ef14221e8bfd07196a66d6cc8851785 (HEAD -> main, origin/main)
Merge: 163a0d6 b9baf3b
Author: alextisch <58130219+alextisch@users.noreply.github.com>
Date:   Sun Apr 13 20:50:39 2025 +0300

    Merge pull request 
    
    updated hello_world.cpp with comment

commit b9baf3b8233147225363385b16d904b71ed0a4d5 (origin/patch1, patch1)
Author: alextisch <alextisch@gmail.com>
Date:   Sun Apr 13 20:45:27 2025 +0300

    updated hello_world.cpp with comment

commit 163a0d6d08326f626488363c6e8107f92bab2a7a
Merge: 1a28873 24e261c
Author: alextisch <58130219+alextisch@users.noreply.github.com>
Date:   Sun Apr 13 20:44:13 2025 +0300

    Merge pull request 
    
    updated hello_world.cpp without bad code style

commit 24e261c84d7447ee5bae0db1762395fc8d36a7f2
Author: alextisch <alextisch@gmail.com>
Date:   Sun Apr 13 20:33:33 2025 +0300

    updated hello_world.cpp without bad code style

commit 1a288739b7207bc0791471b376f62226a9735e1d
Author: alextisch <alextisch@gmail.com>
Date:   Sun Apr 13 20:24:46 2025 +0300

    updated hello_world.cpp with bad code style

commit f2b3840e8d827a7ef3dc8133bbea09144250cfe7
Author: alextisch <alextisch@gmail.com>
Date:   Sun Apr 13 20:13:27 2025 +0300

    added hello_world.cpp with bad code style

commit 1d94cb7d8b2a3b265c5066f191ca0cc1c28b5ac0
Author: alextisch <alextisch@gmail.com>
Date:   Sun Apr 13 20:05:09 2025 +0300

    added LICENSE

commit a542c7d5e0190a336a07ca7be5edf7af649b6c00
Author: alextisch <alextisch@gmail.com>
Date:   Sun Apr 13 20:02:14 2025 +0300

    first commit
```
12. Удалите локальную ветку `patch1`.
```sh
$ git branch -d patch1 
Deleted branch patch1 (was b9baf3b).
```

### Часть 3

**Note:** *Работать продолжайте с теми же репоззиториями, что и в первой части задания.*
1. Создайте новую локальную ветку `patch2`.
```sh
$ git checkout -b patch2
Switched to a new branch 'patch2'
```
2. Измените *code style* с помощью утилиты [**clang-format**](http://clang.llvm.org/docs/ClangFormat.html). Например, используя опцию `-style=Mozilla`.
```sh
$ clang-format -style=Mozilla -i hello_world.cpp
```
3. **commit**, **push**, создайте pull-request `patch2 -> master`.
```sh
$ git status            
On branch patch2
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   hello_world.cpp

no changes added to commit (use "git add" and/or "git commit -a")
$ git commit -a -m "updated hello_world.cpp with clang-format"
[patch2 042d850] updated hello_world.cpp with clang-format
 1 file changed, 8 insertions(+), 6 deletions(-)
$ git push -u origin patch2                                   
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 16 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 369 bytes | 369.00 KiB/s, done.
Total 3 (delta 2), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
remote: 
remote: Create a pull request for 'patch2' on GitHub by visiting:

remote: 

 * [new branch]      patch2 -> patch2
branch 'patch2' set up to track 'origin/patch2'.
"Able to merge" -> "Create pull request"
```
4. В ветке **master** в удаленном репозитории измените комментарии, например, расставьте знаки препинания, переведите комментарии на другой язык.
```
done
```
5. Убедитесь, что в pull-request появились *конфликтны*.
```
"This branch has conflicts that must be resolved"
```
6. Для этого локально выполните **pull** + **rebase** (точную последовательность команд, следует узнать самостоятельно). **Исправьте конфликты**.
```sh
$ git checkout patch2
Already on 'patch2'
Your branch is up to date with 'origin/patch2'.
$ git pull --rebase origin main  
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 3 (delta 2), reused 0 (delta 0), pack-reused 0 (from 0)
Unpacking objects: 100% (3/3), 1.01 KiB | 1.01 MiB/s, done.
 * branch            main       -> FETCH_HEAD
   2486fd5..78cf26a  main       -> origin/main
Auto-merging hello_world.cpp
CONFLICT (content): Merge conflict in hello_world.cpp
error: could not apply 042d850... updated hello_world.cpp with clang-format
hint: Resolve all conflicts manually, mark them as resolved with
hint: "git add/rm <conflicted_files>", then run "git rebase --continue".
hint: You can instead skip this commit: run "git rebase --skip".
hint: To abort and get back to the state before "git rebase", run "git rebase --abort".
hint: Disable this message with "git config advice.mergeConflict false"
Could not apply 042d850... updated hello_world.cpp with clang-format
$ git add hello_world.cpp
$ git rebase --continue                                          
[detached HEAD 7d67482] updated hello_world.cpp with clang-format
 1 file changed, 11 insertions(+)
Successfully rebased and updated refs/heads/patch2.

```
7. Сделайте *force push* в ветку `patch2`

```sh
$ git push --force-with-lease origin patch2
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 16 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 565 bytes | 565.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.

8. Убедитель, что в pull-request пропали конфликтны.
```
"No conflicts with base branch"
```
9. Вмержите pull-request `patch2 -> master`.
```
"Merge pull request"
```

10. Git log
```sh
$ git log                                  
commit 7d67482d520f9228dab56cc935ebd7b19de8f552 (HEAD -> patch2, origin/patch2)
Author: alextisch <alextisch@gmail.com>
Date:   Sun Apr 13 20:58:12 2025 +0300

    updated hello_world.cpp with clang-format

commit 78cf26a9ceb1c3a94da4d43e712d6fef6513de9b (origin/main)
Author: alextisch <58130219+alextisch@users.noreply.github.com>
Date:   Sun Apr 13 21:01:27 2025 +0300

    Update hello_world.cpp с комментариями

commit 2486fd5b2ef14221e8bfd07196a66d6cc8851785 (main)
Merge: 163a0d6 b9baf3b
Author: alextisch <58130219+alextisch@users.noreply.github.com>
Date:   Sun Apr 13 20:50:39 2025 +0300

    Merge pull request 
    
    updated hello_world.cpp with comment

commit b9baf3b8233147225363385b16d904b71ed0a4d5 (origin/patch1)
Author: alextisch <alextisch@gmail.com>
Date:   Sun Apr 13 20:45:27 2025 +0300

    updated hello_world.cpp with comment

commit 163a0d6d08326f626488363c6e8107f92bab2a7a
Merge: 1a28873 24e261c
Author: alextisch <58130219+alextisch@users.noreply.github.com>
Date:   Sun Apr 13 20:44:13 2025 +0300

    Merge pull request 
    
    updated hello_world.cpp without bad code style

commit 24e261c84d7447ee5bae0db1762395fc8d36a7f2
Author: alextisch <alextisch@gmail.com>
Date:   Sun Apr 13 20:33:33 2025 +0300

    updated hello_world.cpp without bad code style

commit 1a288739b7207bc0791471b376f62226a9735e1d
Author: alextisch <alextisch@gmail.com>
Date:   Sun Apr 13 20:24:46 2025 +0300

    updated hello_world.cpp with bad code style

commit f2b3840e8d827a7ef3dc8133bbea09144250cfe7
Author: alextisch <alextisch@gmail.com>
Date:   Sun Apr 13 20:13:27 2025 +0300

    added hello_world.cpp with bad code style

commit 1d94cb7d8b2a3b265c5066f191ca0cc1c28b5ac0
Author: alextisch <alextisch@gmail.com>
Date:   Sun Apr 13 20:05:09 2025 +0300

    added LICENSE

commit a542c7d5e0190a336a07ca7be5edf7af649b6c00
Author: alextisch <alextisch@gmail.com>
Date:   Sun Apr 13 20:02:14 2025 +0300

    first commit
```
