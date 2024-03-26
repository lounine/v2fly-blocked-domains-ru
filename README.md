# Списки заблокированных в РФ доменов в формате xray / v2ray
Родные власти в постоянной заботе о несознательных россиянах блокируют множество сайтов, на которые нам совершенно незачем ходить. Долг каждого сознательного гражданина – помочь Родине в этом нелёгком деле. Этот репозиторий – попытка собрать список всех запрещённых доменов, на которые в минуты слабости может захотеться зайти. Используйте его, чтобы ещё надёжнее заблокировать всё запретное.

## Источники и структура данных
В файл **ru-blocked.dat** попадают:
- в раздел `antifilter-community` – все домены из списка **Community** проекта [Antifilter](https://antifilter.download)
- в раздел `itdoginfo-inside` – все домены из списка **src/Russia-domains-inside.lst** репозитория [@itdoginfo/allow-domains](https://github.com/itdoginfo/allow-domains)
- в раздел `itdoginfo-outside` – все домены из списка **src/Russia-domains-outside.lst** репозитория [@itdoginfo/allow-domains](https://github.com/itdoginfo/allow-domains)
- в раздел `all` – все недоступные из РФ домены из всех списков выше
- в раздел `all-outside` – все недоступные из-за пределов РФ российские домены из всех списков выше

## Установка

### Вручную
Скачать файл ru-blocked.dat из последнего релиза и поместить его в папку `/usr/share/xray`, `/usr/share/v2ray`, `/usr/local/share/xray` или `/usr/local/share/v2ray`, в зависимости от места установки xray/v2ray.

### Скачать и обновить все списки доменов до последней версии:
```bash
curl -fsSL 'https://github.com/lounine/ru-blocked-domains/releases/latest/download/update-geosites.sh' \
  | sudo bash
```

Скрипт автоматически установит списки доменов в стандартную папку xray/v2ray в `/usr/share/...` или `/usr/local/share/...`. 
Нестандартную место установки можно передать в качестве параметра:
```bash
curl -fsSL 'https://github.com/lounine/ru-blocked-domains/releases/latest/download/update-geosites.sh' \
  | sudo bash -s -- -g /some/other/location/
```

### Настройка автоматического обновление списков доменов
Для автоматического ежедневного обновления списков предлагается запускать тот же скрипт через cron. Релиз собирается к 21:00 UTC (00:00 MSK), а cron.daily запускается на большинстве систем около 6:00 - 7:00, и  как раз подхватит последнюю версию.
```bash
sudo curl -fsSL 'https://github.com/lounine/ru-blocked-domains/releases/latest/download/update-geosites.sh' \
  | sudo install /dev/stdin /etc/cron.daily/update-geosites
```

И при необходимости обновить немедленно:
```
sudo /etc/cron.daily/update-geosites
```
