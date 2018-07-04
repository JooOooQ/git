# git

При работе с GitHub Desktop возникла следующая ошибка:<br>
fatal: unable to access 'https://github.com/JooOooQ/git.git/': schannel: next InitializeSecurityContext failed: Unknown error (0x80092012)<br>
Ошибка возникала при любых попытках соединится с github сервером (в частности я не мог склонировать репозиторий).
Оказалось, что дело в антивирусе Касперского.<br>
Выхода на текущий момент нашёл только два:
- либо в настройках Касперского -> Дополнительно -> Сеть выставить "Не проверять защищенные соединения"
- либо в репозитории выполнить команду git config http.sslVerify "false"

Также есть глобальный флаг для всех репозиториев, команда<br>
git config --global http.sslVerify "false"<br>

Теперь немного о настройке SSH ключа.<br>
Сгенерировать ключ под Windows мне помогла вот эта статья:<br>
https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/<br>
Команды выполняются в Git Bash, который вроде бы устанавливается вместе с GitHub Desktop. Но не могу сказать точно, у меня он уже был установлен. Если что, установщик скачивается отсюда https://git-scm.com/downloads.<br>

Если всё сделаете правильно ключики сгенерятся по умолчанию в<br>
C:\\Users\\"YOUR_USER_NAME"\\.ssh<br>
где вместо "YOUR_USER_NAME" ваше имя пользователя.<br>
Скопировать ключик в буфер обмена можно командой<br>
clip < ~/.ssh/id_rsa.pub<br>
Далее следуйте шагам описанным здесь<br>
https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/<br>

Одна вещь в статье упущена. Это то, что папка в которой лежит ключ, должна также содержать файл known_hosts.<br>
В нём у меня прописано<br>
github.com,192.30.253.113 "SSH KEY"<br>
192.30.253.112 "SSH KEY"<br>
где вместо "SSH KEY" ваш ключ.


