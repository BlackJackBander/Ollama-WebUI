# Ollama WebUI для Termux

Веб-интерфейс для локальной модели gemma3:1b через Ollama API.

## Установка

### 1. На Termux: создать папку для сайта
```bash
mkdir -p ~/www/ollama-webui
```

### 2. Скопировать файлы
```bash
# Через ADB (с компьютера)
adb push ollama-webui/. /data/data/com.termux/files/home/www/ollama-webui/

# Или через SCP (нужен openssh в Termux)
scp -r ollama-webui/* termux@192.168.1.100:~/www/ollama-webui/
```

### 3. Настроить nginx
```bash
# Скопировать конфиг
cp ~/www/ollama-webui/ollama.conf ~/.termux/nginx/conf.d/

# Или добавить в основной конфиг:
# В /data/data/com.termux/files/usr/etc/nginx/nginx.conf
# в блок http добавить:
include /data/data/com.termux/files/home/www/ollama-webui/ollama.conf;

# Перезапустить nginx
nginx -s reload
```

### 4. Узнать IP Termux
```bash
ifconfig wlan0 | grep inet
```

### 5. Открыть в браузере
```
http://<IP_TERMUX>:8080
```

## Настройки

- **IP адрес Ollama** - IP устройства с Termux (по умолчанию 192.168.1.100)
- **Temperature** - креативность ответов (0.0-2.0)
- **Max tokens** - максимальная длина ответа

## Возможности

- Потоковая генерация ответов (real-time)
- Индикатор статуса подключения
- История сообщений в сессии
- Подсветка кода в ответах
- Адаптивный дизайн
- Остановка генерации
