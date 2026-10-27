---
title: Главная
permalink: /
---

# Документация проекта

Parts Unlimited Lite — учебный проект по программной инженерии. Здесь опубликованы инструкции для участников команды и описания выбранного окружения.

**Редакция публикации: 1.1.** Страница обновлена коммитом в исходном репозитории после первой публикации.

## Разделы

- [Начало работы]({{ '/start.html' | relative_url }}) — доступ к проекту и правила изменения документации.
- [Окружение разработки]({{ '/environment.html' | relative_url }}) — платформа Mac M1 и планируемый стек.
- [Наша команда]({{ '/Our-team.html' | relative_url }}) — роли участников и назначение ресурсов.
- [Предстоящие события]({{ '/events/' | relative_url }}) — учебные примеры связанных страниц.

## О публикации

Этот сайт формируется GitHub Pages из Markdown-файлов в папке `docs` репозитория `parts-unlimited-docs`. Изменения публикуются после коммита в ветку `main`.

Wiki и сайт документации используют отдельные хранилища. Изменение Wiki само по себе не изменяет этот сайт.

## Статус проекта

В текущей работе подготовлена документация. Приложение, база данных и конвейер доставки приложения будут реализованы в следующих практических работах.



flowchart TD
    %% Группировка репозиториев
    subgraph GitHubRemote ["Удаленный репозиторий GitHub"]
        direction LR
        subgraph MainRepo ["Репозиторий: parts-unlimited-docs"]
            MainBranch["Ветка: main"]
            DocsFolder["Папка: /docs"]
            MainBranch ---> DocsFolder
        end
        
        subgraph WikiRepo ["Репозиторий: parts-unlimited-docs.wiki"]
            WikiPages["Markdown файлы (.md)"]
            Sidebar["Навигация (_Sidebar.md)"]
        end
    end

    %% Локальная машина
    subgraph LocalMachine ["Рабочая платформа (Mac M1)"]
        LocalGit["Локальный Git-клиент"]
    end

    %% Процесс автоматизации публикации
    subgraph Hosting ["Хостинг сайтов"]
        GHAction["GitHub Actions (Сборка Jekyll)"]
        GHPages["GitHub Pages (https://github.io...)"]
    end

    %% Взаимодействие
    LocalGit --->|git push main| MainBranch
    LocalGit --->|git push wiki| WikiRepo
    
    DocsFolder --->|Триггер коммита| GHAction
    GHAction --->|Публикация артефактов| GHPages
