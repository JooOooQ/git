# git

При работе с **GitHub Desktop** возникла следующая ошибка:
>fatal: unable to access 'https://github.com/JooOooQ/git.git/': schannel: next InitializeSecurityContext failed: Unknown error (0x80092012)

Ошибка возникала при любых попытках соединится с github сервером (в частности я не мог склонировать репозиторий).

Выяснилось, что дело в **антивирусе Касперского**. Выхода на текущий момент нашёл только два:
- либо в настройках Касперского -> Дополнительно -> Сеть

    выставить: **Не проверять защищенные соединения**
- либо в репозитории проекта выполнить команду
```shell    
    git config http.sslVerify "false"
```

Также есть глобальный флаг для всех репозиториев, команда
```shell
git config --global http.sslVerify "false"
```

Теперь немного о настройке **SSH ключа**.

Сгенерировать ключ под **Windows** мне помогла вот эта статья:

https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/

Команды выполняются в **Git Bash**, который вроде как устанавливается вместе с **GitHub Desktop**. Но если что, официальный установщик можно скачать также отсюда https://git-scm.com/downloads.

Если всё сделаете правильно, ключики сгенерируются по умолчанию в
```
C:\\Users\\<YOUR_USER_NAME>\\.ssh
```
где вместо `<YOUR_USER_NAME>` ваше имя пользователя.

Скопировать ключик в буфер обмена можно командой
```shell
clip < ~/.ssh/id_rsa.pub
```

Далее следуйте шагам описанным здесь

https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/

Одна вещь в статье упущена. Это то, что папка в которой лежит ключ, должна также содержать файл **known_hosts**.

В нём у меня прописано
```
github.com,192.30.253.113 <SSH KEY>
192.30.253.112 <SSH KEY>
```
где вместо `<SSH KEY>` ваш ключ шифрования.
