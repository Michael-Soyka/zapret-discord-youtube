# Zapret (обход блокировки Discord'а и YouTube'а)

> [!NOTE]  
> Данный репозиторий — **некоммерческая** *User-Friendly* сборка [оригинального репозитория](https://github.com/bol-van/zapret). Здесь используются оригинальные бинарники, сравнить которые вы можете с помощью хэша.
> 
> Так как zapret — open-source, вы всегда можете сами собрать эти бинарники и не бояться вирусов.
> 
> **Буду рад [⭐ поставленной репозиторию звезде](https://github.com/kartavkun/zapret-discord-youtube/stargazers) (в правом верхнем углу) 🙂**

## Лицензия

Этот проект распространяется на условиях лицензии MIT.  
Полный текст лицензии можно найти в файле [LICENSE](./LICENSE).

## Установка и использование

### Установка на Linux

Для удобства установки и настройки zapret на Linux был создан автоматизированный скрипт. Следуйте инструкциям ниже:

> [!TIP]  
> Установите **curl** для скачивания и запуска скрипта

**Скачайте и запустите скрипт установки:**

   ```bash
   bash <(curl -s https://raw.githubusercontent.com/kartavkun/zapret-discord-youtube/main/setup.sh)
   ```

  Если не работает, то запустите другую команду ([Спасибо, RekQu](https://github.com/kartavkun/zapret-discord-youtube/discussions/16#discussioncomment-13573048)):
  ```bash
  bash <(curl -s https://raw.githubusercontent.com/kartavkun/zapret-discord-youtube/main/setup.sh | psub)
  ```

Этот скрипт:

- Установит необходимые зависимости (wget, git).

- Скачает последний релиз zapret из [оригинального репозитория](https://github.com/bol-van/zapret).

- Клонирует этот репозиторий с конфигами.

- Запустит интерактивное меню для выбора конфигурации.

Для пользователей NixOS доступен flake с декларативной настройкой:

>[!NOTE]
> для поддержки flake в nixos пропишите в файле `/etc/nixos/configuration.nix` (см. подробнее [Flakes](https://wiki.nixos.org/wiki/Flakes/ru))
>
```nix
nix.settings.experimental-features = [ "nix-command" "flakes" ];
```

```nix
# В вашем flake.nix (можете его поместить в /etc/nixos/flake.nix)
{
  description = "NixOS configuration with zapret-discord-youtube";

  inputs = {
    nixpkgs.url = "github:NixOS/nixpkgs/nixos-unstable";
    zapret-discord-youtube.url = "github:kartavkun/zapret-discord-youtube;
  };

  outputs = { self, nixpkgs, zapret-discord-youtube }: {
    nixosConfigurations.nixos = nixpkgs.lib.nixosSystem {
      system = "x86_64-linux";
      modules = [
        ./configuration.nix
        zapret-discord-youtube.nixosModules.default
        {
          services.zapret-discord-youtube = {
            enable = true;
            config = "general(ALT)";  # или любой конфиг из configs (general, general(ALT), general (SIMPLE FAKE) и т.д.)
          };
        }
      ];
    };
  };
}
```

### Использование

1. **Выберите конфиг:**

После запуска скрипта появится меню с выбором конфигурации. Выберите подходящий вариант:

- general — базовая конфигурация для обхода блокировок Discord и YouTube.

- general_ALT, general_ALT2, и т.д. — альтернативные конфигурации, если базовая не работает.

- general_MGTS, general_MGTS2 — конфигурации для провайдера МГТС.

Для смены конфига напишите следующую команду

```bash
$HOME/zapret-configs/install.sh
```

2. Завершение установки:

После выбора конфигурации **БЕЙТЕ ПО КНОПКЕ ENTER ПОКА НЕ БУДЕТ ПРИГЛАШЕНИЯ ТЕРМИНАЛА**.

## Решение проблем

- Проверьте права доступа: Убедитесь, что скрипт запускается с правами root или через sudo.

- Не работает обход? Попробуйте выбрать другую конфигурацию из списка.

- Проблемы с зависимостями: Если скрипт не может установить wget, установите его вручную с помощью пакетного менеджера вашего дистрибутива.

## Остановка и удаление

Чтобы остановить zapret, выполните:

```bash
sudo /opt/zapret/uninstall_easy.sh
```

## Добавление дополнительных адресов заблокированных сайтов

Если хотите обойти другие сайты, то я написал [гайд от себя](https://github.com/kartavkun/zapret-discord-youtube/discussions/2#discussion-7902158). Если есть люди более знающие, то я приму конструктивную критику :D

## Проверено на:
- [Arch Linux](https://archlinux.org/) (i use Arch btw)
- [Void Linux](https://voidlinux.org/)
- [Slackware Linux](http://www.slackware.com/)
- [Alpine linux](https://www.alpinelinux.org/)
- [Solus](https://getsol.us/)
- [AntiX Linux](https://antixlinux.com/)
- [Pop!_OS](https://system76.com/pop/)
- [Ubuntu 18.04+](https://ubuntu.com/)
- [Kubuntu](https://kubuntu.org/)
- [NixOS](https://nixos.org/) (через flake)

## Поддержка

Вы можете поддержать проект, поставив :star: (сверху справа этой страницы)!
Лучше всего [задонатьте мне денюжку](https://t.me/kartavslinks/8) :) 

Также, вы можете поддержать разработчика оригинального репозитория zapret тут — https://github.com/bol-van/zapret/issues/590
<a href="https://star-history.com/#kartavkun/zapret-discord-youtube&Date"> <picture> <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/svg?repos=kartavkun/zapret-discord-youtube&type=Date&theme=dark" /> <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/svg?repos=kartavkun/zapret-discord-youtube&type=Date" /> <img alt="Star History Chart" src="https://api.star-history.com/svg?repos=kartavkun/zapret-discord-youtube&type=Date" /> </picture> </a>

## Благодарности

- Большое спасибо [bol-van](https://github.com/bol-van/), создателю оригинального репозитория [zapret](https://github.com/bol-van/zapret/).

- Благодарность [Flowseal](https://github.com/Flowseal) за конфигурации, которые были адаптированы для этого репозитория.

Примечания

- Если у вас возникли проблемы с использованием zapret на Linux, задавайте вопросы в [оригинальном репозитории](https://github.com/bol-van/zapret/issues), предоставляя конфиг из `/opt/zapret/config`.

- Этот репозиторий предназначен для упрощения настройки zapret на Linux. Все вопросы, связанные с Windows, следует задавать в [репозитории Flowseal](https://github.com/Flowseal/zapret-discord-youtube).
