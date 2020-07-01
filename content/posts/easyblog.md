+++
title = "Бложик на изи"
author = "Михаил Мариненко"
authorTwitter = "0x77dev"
tags = ["hugo", "blog", "netlify", "git", "ci", "cd"]
keywords = ["hugo", "blog", "netlify", "git", "ci", "cd"]
description = "Как поднять свой блог быстро и очень просто..."
showFullContent = false
+++

# Бложик на изи
Сидел я такой, гуглил, и увидел прикольную херню на golang, под названием **Hugo**.

Он показался мне прикольным, вот я и подумал замутить блог в котором вы это читаете.

## Приступаем к разворачиванию и настройке 
### Настройка Hugo и Репозитория
1. Установите [Hugo](https://gohugo.io/getting-started/quick-start/#step-1-install-hugo)
2. Пройтиде [туториал](https://gohugo.io/getting-started/quick-start) и настройте его под себя
3. Заведем Git репозитроий к примеру в GitHub.
4. Инитим репу и пушим усе туда.
    ```shell
    $ git init 
    $ git add .
    $ git commit -am "init"
    $ git push origin master -u
    ```

### Настройка Netlify
1. Регаемся на Netlify
2. Создаем сайтик 
3. Выбираем Github/или что у вас там ![Netlify](https://d33wubrfki0l68.cloudfront.net/188f9bfa9eb4997757414ec0ac1979d7111c9741/8f7a6/images/hosting-and-deployment/hosting-on-netlify/netlify-create-new-site-step-2.jpg)
4. Выбираем репозиторий
5. Кляцаем у перед и готово!
    * > Netlify сам поймет что вы используете Hugo, по этому просто жмякаем дальше/или да и все.

# Ошибки которые возникли у меня
Моя тема [Terminal](https://github.com/panr/hugo-theme-terminal/) требует более новую чем дефолтная версия Hugo у Netlify.

По этому 

Просто помещаем файлик в корень проета и называем его `netlify.toml`

и вставляем вот это внутырь файлика:
```toml
[build]
publish = "public"
command = "hugo --gc --minify"

[context.production.environment]
HUGO_VERSION = "0.73.0"
HUGO_ENV = "production"
HUGO_ENABLEGITINFO = "true"

[context.split1]
command = "hugo --gc --minify --enableGitInfo"

[context.split1.environment]
HUGO_VERSION = "0.73.0"
HUGO_ENV = "production"

[context.deploy-preview]
command = "hugo --gc --minify --buildFuture -b $DEPLOY_PRIME_URL"

[context.deploy-preview.environment]
HUGO_VERSION = "0.73.0"

[context.branch-deploy]
command = "hugo --gc --minify -b $DEPLOY_PRIME_URL"

[context.branch-deploy.environment]
HUGO_VERSION = "0.73.0"

[context.next.environment]
HUGO_ENABLEGITINFO = "true"
```

Можете поменять на версию которая вам нужна, и все! :3
