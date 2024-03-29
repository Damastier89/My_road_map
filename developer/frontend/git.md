# GIT

- [Объектная модель Git](#object-model)
- [Three Trees](#three-trees)
- [Отмена изменений](#canceling-changes)
- [Изменение истории коммитов](#edit-commit-history)
- [Отмена слияния](#annul-merger)
- [Что такое HEAD и detached HEAD?](#head)
- [Что такое Git flow?](#git-flow)

`Git` — система управления версиями с распределенной архитектурой и абсолютный лидер по популярности среди современных систем управления версиями.

> Это развитый проект с активной поддержкой и открытым исходным кодом.
> Система Git была изначально разработана в 2005 году Линусом Торвальдсом — создателем ядра операционной системы Linux.
> Git применяется для управления версиями в рамках колоссального количества проектов по разработке ПО, как коммерческих, так и с открытым исходным кодом.
> Система используется множеством профессиональных разработчиков программного обеспечения.
> Она превосходно работает под управлением различных операционных систем и может применяться со множеством интегрированных сред разработки (IDE).

### Working directory, Staging area и Repository

> Эти термины касаются систем контроля версий, таких как Git, и используются в процессе управления изменениями в проекте.

> Рабочий каталог `Working directory` - это текущий рабочий каталог проекта, в котором вы вносите изменения в файлы проекта.

> Область подготовки `Staging area`, также известная как индекс, является промежуточной областью, где вы определяете, какие изменения ваших файлов должны быть внесены в следующую ревизию проекта.

> Хранилище `Repository` - это место, где сохраняются все версии файлов вашего проекта, включая их историю изменений. Здесь вы можете отслеживать изменения в вашем проекте, возвращаться к предыдущим версиям, сравнивать изменения между версиями и т.д.

> Таким образом, рабочий каталог - это ваш рабочий инструмент, предназначенный для внесения изменений в проект, область подготовки - промежуточный этап, где вы определяете, какие изменения следует включить в следующую ревизию проекта, а хранилище - это место, где они действительно сохраняются и могут быть отслежены в будущем

### `.gitignore`

> Файл `.gitignore` содержит список шаблонов (пути и имена файлов и папок), которые Git должен игнорировать при работе с репозиторием. Если вы добавите файлы в этот файл, то при выполнении команды git add или git commit они будут проигнорированы, а Git не будет их коммитить или отображать в статусе изменений.

### `git config`

> Команда git config используется для установки и получения параметров конфигурации Git, которые применяются на уровне глобальной конфигурации пользователя, репозитория и текущей сессии Git.

В частности, с помощью команды git config можно выполнять следующие задачи:

- установить и получить пользовательское имя и электронную почту, используемые для атрибуции коммитов;
- изменить поведение Git, такое как дефолтное количество строк контекста в результатах команды git diff или настройки форматирования логов;
- добавлять, изменять и удалять алиасы команд Git для удобства использования.

Три уровня конфигурации в Git:

- Глобальный уровень: устанавливает общие настройки для текущего пользователя, которые будут применяться ко всем репозиториям, с которыми пользователь работает на данной машине. Конфигурация на этом уровне хранится по умолчанию в файле `~/.gitconfig`.
- Уровень репозитория: определяет настройки конкретного репозитория Git. Эта конфигурация хранится в файле `.git/config` в корневой папке репозитория и применяется только к данному репозиторию.
- Уровень командной строки: определяет временные изменения в конфигурации Git, применяемые только для текущего запуска команды Git. Он может использоваться, например, для перезаписи настроек Git в процессе автоматизации или для переопределения частной настройки репозитория для одной команды.

### Команды fetch и merge

> Команды `fetch` и `merge` - это две основные команды Git, которые используются для обновления локальной копии репозитория до последней версии из удаленного репозитория.

- Команда `fetch` позволяет получить все изменения, которые были добавлены в удаленный репозиторий с момента последней синхронизации, и добавить их в ваш локальный репозиторий, но без апдейта локальных веток, что значит, что вы не будете перескакивать на новую версию кода. То есть после команды fetch, если вы сделаете git status, то увидите, что ваша локальная версия все еще та же самая, что и до команды fetch.

- Команда `merge` позволяет объединить изменения из удаленного репозитория с вашим локальным репозиторием, что приведет к изменению локальных веток. То есть команда merge совмещает исходную ветку, какой-нибудь другой, с вашей текущей веткой, с тем чтобы ваши локальные изменения сбрасывались в новую версию и ваш репозиторий становился синхронизированным с удаленным репозиторием. В результате могут появляться конфликты слияния, которые нужно разрешать.

> Обычно эти команды используются в паре: сначала fetch, чтобы получить изменения из удаленного репозитория, и затем merge, чтобы объединить их с вашим локальным репозиторием. Это позволяет вам получать и использовать последние изменения, внесенные другими участниками проекта.

### fast-forward merge

> `Fast-forward` merge это способ объединения веток в Git, который по умолчанию используется при наличии линейной истории изменений (то есть, когда ветка, на которую выполняется слияние, находится непосредственно впереди текущей в структуре репозитория). При выполнении fast-forward merge Git просто перемещает указатель текущей ветки вперед, к той же самой точке, в которой находится ветка, с которой выполняется слияние, что позволяет сохранить линейную историю изменений без создания новых коммитов.

- Флаг `--squash` используется при слиянии веток (merge), чтобы объединить все коммиты из ветки в один коммит, который затем можно смержить в другую ветку. Это полезно, когда вы хотите сохранить линейную историю коммитов. В частности, --squash избегает создания полного слияния коммитов из ветки, которую вы вливаете.

- Флаг `--no-ff` используется для отключения fast-forward в слиянии. Он заставляет Git создавать новый коммит-слияние, даже если он мог бы выполнить fast-forward. Это полезно, когда вы хотите учитывать историю всех слияний. Кроме того, это сделать необходимым компанию за соблюдение той или иной схемы слияний или для того, чтобы оставить запись в истории коммитов, что две ветки были объединены, даже если возможно было выполнение быстрого forward автоматически.

> В целом, использование этих флагов дает более полный и точный контроль над процессом слияния и историей коммитов в вашем репозитории.

### Pull Request (PR) или Merge Request (MR)

> Pull Request (PR) или Merge Request (MR) - это механизм, используемый в системах контроля версий, таких как Git или GitHub, для обмена изменениями между разными ветками репозитория или между разными репозиториями.

Когда разработчик хочет внести изменения в проект, проходит следующие стадии:

1. Создание новой ветки – ветка создается на основе основной ветки репозитория, например, master, в которой разработчик будет менять и добавлять файлы.
2. Внесение изменений - разработчик вносит требуемые изменения в файлы в рамках своей ветки.
3. Создание `Pull Request/Merge Request` - после завершения работы, разработчик создает запрос на слияние изменений с основной веткой. В PR/MR указывается: какие изменения внесены, какие и зачем файлы изменились, к кому этот Pull Request адресован, а также комментарии и подробное описание работы.
4. `Code review` - После создания `PR/MR` код предоставляется на рассмотрение других разработчиков, которые могут оставить комментарии и советы по улучшению кода.
5. Мержинг - Если все комментарии учтены и изменения одобрены другими разработчиками, менеджер проекта или администратор сливает изменения в основную ветку репозитория.

> `Pull Request/Merge Request` являются важной частью современной методологии разработки программных продуктов, так как они позволяют контролировать процесс слияния изменений, уменьшая ошибки и конфликты, и облегчая сборку кода и релизы.

### Команды для управления git

`git config --global user.name "NAME"` - добавить имя пользователя в git.

`git config --global user.email example@example.ru` - добавить почту пользователя в git.

`git log` - Просмотр истории коммитов с подробной информацией.

`git rebase` — Способ перенести изменения из одной ветки в другую. В отличие от `merge`, перемещение перезаписывает историю. В процессе устраняется нежелательная история.

`fast-forward` - Другими словами, если коммит сливается с тем, до которого можно добраться двигаясь по истории прямо, Git упрощает слияние просто перенося указатель ветки вперед, так как нет расхождений в изменениях.

`git cherry-pick` - Команда git cherry-pick используется для перенесения отдельных коммитов из одного места репозитория в другое, обычно между ветками разработки и обслуживания. Этот механизм отличается от привычных команд git merge и git rebase, которые переносят коммиты целыми цепочками

`git bisect` - На каждом этапе он пытается сократить количество потенциально плохих ревизий вдвое.

`git hooks` — Скрипты оболочки, которые запускаются автоматически до или после того, как Git выполняет важную команду, такую как Commit или Push.

`git clone` — Скачать из удаленно репозитория проект.

`git pull` — Обновить проект, после внесения изменения его другим разработчиком.

`git checkout -b «branchName»` - копирует и переносит всё в новую ветку.

`git checkout -b recevered «branchName»` - восстановить удаленную ветку(локально)

`git branch -d(-D) «branchName»` - удалить ветку.

`git branch -M «branchName»` - изменить название ветки.

`git commit --amend --no-edit` - оставить то же имя коммита, но перезаписать содержимое.

`git commit --amend -m«Name»` - изменить имя последнего коммита.

`git merge master «branchName»` - перенести изменения из одной ветки в другую.

> Плюсы: сохраняет полную историю и хронологический порядок, поддерживает контекст ветки.

> Минусы: история коммитов может быть заполнена (загрязнена) множеством коммитов, отладка с использованием git bisect может стать сложнее.

`git reset HEAD~` - отменить последний коммит, но сохранить изменения.

`git reset` --hard HEAD~(хеш ветки) - удалить последний коммит и откатить изменения.

`git reset` --hard master@{"10 minutes ago"} - cброс к определенному моменту времени.

`git diff` - просмотр не индексированных изменений.

`git reflog` — посмотреть хеши и логи.

`git stash` – спрятать изменения.

`git stash pop` – достать изменения

`git stash --keep-index` - в stash уйдут все изменения кроме тех что уже добавлены в индекс(подготовлены для комита).

### Git Style

`Name_project/fix/task_name` – Именование ветки для fix-bag.

`Name_project/feature/task_name` – Именование для ветки с новым функционалом.

`Name_project/refactor/task_name` – Именование для ветки для правки кода.

`git commit -m"fix(‘component name’): 'task name' ‘текс коммита’."` --no-verify – Так выглядит коммит если фиксился баг. (--no-verify – используется опционально, если husky не пропустил)

`git commit -m"feat(‘component name’): 'task name' ‘текс коммита’."` – Так выглядит коммит если добавили новый функционал.

`git commit -m"refactor(‘component name’): 'task name' ‘текс коммита’."` – Так выглядит коммит если привили код.

### Git problem

`git config --system core.longpaths true` – если возникла проблема «Filename too long»

## Object model

> Объектная модель Git является основой для хранения и управления версиями файлов в системе контроля версий Git. Она состоит из нескольких типов объектов, включая blob (файлы), tree (деревья), commit (коммиты) и tag (теги).

Blob (файл):

- Blob представляет собой содержимое файла в системе Git. Он представляет собой неизменяемый объект, который хранит только данные файла, но не его имя или путь. Каждый файл в репозитории Git представлен в виде отдельного blob.

Tree (дерево):

- Tree представляет собой структуру директорий и файлов. Он содержит ссылки на блобы и указывает на связанные деревья, создавая иерархию файловой системы. Таким образом, tree позволяет хранить древовидную структуру файлов и директорий в Git.

Commit (коммит):

- Commit представляет собой моментальный снимок содержимого репозитория. Он содержит ссылку на дерево, представляющее состояние файлов, а также метаданные, включая автора коммита, дату, сообщение и родительские коммиты. Коммиты образуют цепочку, позволяющую отслеживать историю изменений файлов.

Tag (тег):

- Tag представляет собой статическую ссылку на определенный коммит. Он может быть использован для маркировки важных моментов в истории разработки, таких как релизы программного обеспечения или майлстоны. Теги облегчают доступ к конкретным коммитам без необходимости запоминать их идентификаторы.

.pack файлы:

- .pack файлы являются внутренним форматом хранения данных в Git, используемым для оптимизации хранения объектов при выполнении операций слияния и сжатия данных. Они объединяют несколько объектов Git в один файл для более компактного хранения и эффективного использования пространства.

[Вернуться к началу статьи](#git)

---

## Three Trees

`The Three Trees` - это терминология, которая используется для описания основных состояний файлов в системе контроля версий Git. Они называются "The HEAD" (голова), "The Index" (индекс) и "The Working Directory" (рабочий каталог). Давайте рассмотрим каждое из этих состояний:

The HEAD (голова):

- The HEAD - это указатель на текущую ветку в вашем репозитории. Он указывает на последний коммит в выбранной ветке. The HEAD выступает в качестве указателя на текущее состояние вашего проекта.

The Index (индекс):

- The Index, также известный как стэйджинг-область, является промежуточным состоянием файлов между рабочим каталогом и коммитом. Файлы, добавленные в индекс, будут включены в следующий коммит. Вы можете использовать команду git add для добавления файлов в индекс.

The Working Directory (рабочий каталог):

- The Working Directory - это текущее рабочее состояние вашего проекта. Это директория на вашем компьютере, где вы работаете с файлами проекта. Здесь вы можете вносить изменения в файлы, добавлять новые файлы или удалять существующие.

> Взаимодействие между этими тремя состояниями основано на выполнении операций коммита и индексации (стэйджинга) файлов. Когда вы делаете коммит, файлы из индекса записываются в коммит и состояние HEAD обновляется. Когда вы изменяете файлы в рабочем каталоге, вам нужно добавить их в индекс, чтобы они попали в следующий коммит.

[Вернуться к началу статьи](#git)

---

## Canceling changes

> Отмена изменений в Git может выполняться с использованием команды checkout, reset, revert в зависимости от ситуации. Рассмотрим каждый из них в контексте отмены изменений:

checkout:

- Команда `git checkout` позволяет переключаться между ветками или отменять изменения в рабочем каталоге. Она может быть использована для отмены локальных изменений, которые не были добавлены в индекс или созданы коммитом. Например, git checkout -- file.txt вернет файл "file.txt" к его предыдущему состоянию, отменяя незакоммиченные изменения.

reset:

- Команда `git reset` используется для отмены коммитов и перемещения HEAD и веток на определенный коммит. В зависимости от опции, git reset может удалить коммиты и сделать их недоступными для восстановления. Она может применяться для отмены коммитов, которые еще не были опубликованы на удаленном репозитории. Например, git reset HEAD~1 отменит последний коммит и вернет изменения в рабочий каталог.

revert:

- Команда `git revert` создает новый коммит, который отменяет изменения, внесенные в другой коммит. Она может использоваться для отмены изменений, которые уже были опубликованы в удаленном репозитории. git revert commit создаст новый коммит, который отменит изменения, внесенные в указанный коммит.

> Для отмены merge-коммита в Git можно использовать команду `git revert`. Например, git revert -m 1 commit создаст новый коммит, который отменяет все изменения, внесенные в указанный merge-коммит.

> Чтобы узнать родителей merge-коммита, можно использовать команду `git show`. Например, git show --pretty="format:%P" commit покажет идентификаторы родителей указанного merge-коммита.

> Команды `git clean и git rm` используются для удаления файлов из рабочего каталога и индекса соответственно. git clean позволяет очистить рабочий каталог от неотслеживаемых файлов, а git rm используется для удаления файлов из индекса и рабочего каталога.

[Вернуться к началу статьи](#git)

---

## Edit commit history

> Изменение истории коммитов может быть полезным, но требует осторожности, особенно при работе в команде. Вот некоторые команды, которые могут помочь изменить историю коммитов в Git:

commit с флагом --amend:

- Команда `git commit --amend` позволяет внести изменения в последний коммит. Она используется, когда нужно добавить или изменить файлы, исправить сообщение коммита или объединить соответствующие коммиты в один.

cherry-pick:

- Команда `git cherry-pick` позволяет применять коммиты из одной ветки на другую. Она полезна, когда нужно применить определенные коммиты из другой ветки на активную ветку.

filter-branch:

- Команда `git filter-branch` позволяет изменять историю коммитов путем применения фильтров. Она может быть использована для переписывания истории, удаления файлов или изменения авторства коммитов. Однако она считается опасной операцией и должна быть использована с осторожностью.

rebase:

- Команда `git rebase` позволяет перемещать, изменять или объединять коммиты ветки. Она используется для создания чистой и линейной истории коммитов. git rebase -i позволяет работать в интерактивном режиме ребейза.

> Интерактивный режим ребейза (git rebase -i) предоставляет возможность переставлять, объединять, редактировать, удалять или исправлять коммиты в процессе ребейза. Он позволяет контролировать историю коммитов и выполнить различные операции над ними.

> Однако при использовании ребейза следует быть осторожным. Некорректное использование может привести к конфликтам слияния, потере коммитов и изменению истории, что может затруднить работу в команде или восстановление данных.

> Команда `stash` позволяет временно сохранить изменения в рабочем каталоге и индексе, чтобы переключиться на другую ветку без необходимости делать коммит. git stash save используется для сохранения изменений, а git stash apply для их применения.

> `reflog` – это журнал ссылок, который отслеживает изменения указателей (например, HEAD и ветки) в Git. Команда git reflog выводит журнал изменений указателей и позволяет восстановить состояние, которое было до изменений.

[Вернуться к началу статьи](#git)

---

## Annul merger

> Отмена слияния (merge commit) может быть сложной, но возможной. Есть два основных подхода, которые можно использовать для отмены merge commit:

Отмена с помощью git revert:

- Вы можете использовать команду git revert для создания нового коммита, который отменит изменения, внесенные слиянием.
  Для этого вам нужно выполнить команду `git revert -m 1 commit_sha`, где commit_sha - это хэш коммита слияния. Флаг -m 1 указывает, что вы хотите отменить изменения из первого родительского коммита слияния.
  После выполнения этой команды будет создан новый коммит, который компенсирует изменения, внесенные слиянием. История коммитов не изменяется, а вместо этого добавляется новый коммит отмены.

Отмена с помощью git reset:

- Другой способ отмены merge commit - использовать команду git reset. Однако, следует быть предельно осторожным при использовании этой команды, поскольку она изменяет историю коммитов и может привести к потере данных.
  Чтобы отменить merge commit с помощью git reset, вы можете выполнить команду `git reset --hard commit_sha`, где commit_sha - это хэш коммита, предшествующего merge commit.
  При использовании этой команды все изменения, внесенные merge commit и его потомками, будут удалены, а ваша ветка будет указывать на состояние до слияния.

> Оба подхода имеют свои преимущества и риски. Используйте их с осторожностью и всегда делайте резервные копии перед выполнением таких действий, чтобы в случае необходимости восстановить данные.

[Вернуться к началу статьи](#git)

---

## Head

`HEAD` - это указатель на текущую ветку или коммит в Git. Он указывает на последний коммит ветки, на которой вы находитесь. HEAD можно рассматривать как указатель на "голову" текущей ветки.

`Detached HEAD` (отключенная "голова") - это состояние, в котором HEAD указывает не на именованную ветку, а непосредственно на определенный коммит. В этом состоянии вы находитесь в "безымянной" ветке, и все новые коммиты не будут связаны с какой-либо веткой, что может привести к их потере, если не будут сохранены ссылки на них.

`HEAD^` - это указатель на родительский коммит текущего HEAD. Фактически, HEAD^ означает "первого родителя HEAD". Если HEAD указывает на коммит слияния, который имеет несколько родительских коммитов, HEAD^ указывает на первого родителя.

`HEAD~` - это оператор, который используется для обозначения предшествующих коммитов, относительно текущего HEAD. Например, HEAD1 обозначает родительский коммит HEAD, HEAD2 обозначает родительский коммит родительского коммита HEAD, и так далее.

`HEAD@{n}` - это синтаксис, используемый для обращения к предыдущим позициям HEAD в истории. HEAD@{1} обозначает предыдущую позицию HEAD, HEAD@{2} - позицию перед ней, и так далее. Это полезно, когда вам нужно обратиться к предыдущим состояниям HEAD или выполнить операции с коммитами, которые были в них.

[Вернуться к началу статьи](#git)

---

## Git flow

`Git Flow` - это популярная модель ветвления и организации рабочего процесса в Git. Он представляет собой стратегию организации веток и определяет способ взаимодействия между ними, чтобы облегчить совместную работу в команде разработчиков.

Основные ветки в модели Git Flow:

- Master - ветка, которая содержит стабильную и готовую к развертыванию версию продукта.

- Develop - ветка, на которой ведется основная разработка. Из нее создаются фичи и исправления ошибок.

Вспомогательные ветки в модели Git Flow:

- Feature - ветка, создаваемая из ветки Develop для разработки нового функционала. После завершения фичи она сливается обратно в ветку Develop.

- Release - ветка, создаваемая из ветки Develop для подготовки новой версии к выпуску. Здесь могут происходить исправления ошибок и подготовка документации перед релизом. После тестирования она сливается в ветку Master, а также в ветку Develop для сохранения изменений, которые были внесены во время подготовки релиза.

- Hotfix - ветка, создаваемая из ветки Master для быстрого исправления критических ошибок в производственной версии. После исправления она сливается обратно в ветки Master и Develop.

Примеры инструментов, поддерживающих модель Git Flow, включают:

- `Git Flow Extension`: это расширение командной строки, предоставляющее удобный интерфейс для создания и управления ветками в соответствии с Git Flow.
- `SourceTree`: это графический клиент Git, который предоставляет наглядный и интуитивно понятный интерфейс для работы с ветками Git Flow.
- `GitKraken`: это еще один графический клиент Git с поддержкой Git Flow и удобными инструментами для создания и переключения между ветками.

> Git Flow предоставляет удобную и структурированную методологию работы с Git, которая помогает командам разработчиков эффективно совместно работать над проектом.

[Вернуться к началу статьи](#git)

---
