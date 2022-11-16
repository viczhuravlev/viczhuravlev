# WebSocket

>WebSocket — это технология позволяющая установить двухстороннюю(«дуплексную») связь с сервером.

Сервер может открывать соединения WebSocket с несколькими клиентами — даже несколько соединений с одним и тем же клиентом.
Затем он может отправить сообщение одному, нескольким или всем этим клиентам.
Закрыть соединение может и клиент и сервер отправив сообщение «close».
Поддерживается почти всеми современными браузерами API WebSocket.

## In the wild
В каких ситуациях используются WebSocket-ы:
* Chat(чаты)
* Multiplayer Games(игры)
* Collaboration(приложения для совместной работы)
* Developer Tools(инструменты разработчика)
* Location-dependent(карты)

## Protocol
WebSocket — это протокол для отправки и получения сообщений, основанный на TCP, как и HTTP, но протоколы структурирования сообщений различаются. 

Чтобы установить соединение WebSocket с сервером, клиент сначала отправляет HTTP-запрос «рукопожатия» с заголовком обновления, указывая, что клиент желает установить соединение WebSocket. 
Запрос отправляется на ws: или wss:: URI (аналог http или https).
Установка соединения веб-сокетов начинается с обновления HTTP-запроса, который содержит пару заголовков, таких как:
* `Connection: Upgrade` - означает рукопожатие WebSocket
* `Upgrade: WebSocket` - на что поменять HTTP протокол
* `Sec-WebSocket-Key: base64` - содержит случайное значение с использованием кодировки Base64
и все это образует GET-запрос:
```shell
GET ws://websocketexample.com:8181/ HTTP/1.1
Host: localhost:8181
Connection: Upgrade
Pragma: no-cache
Cache-Control: no-cache
Upgrade: websocket
Sec-WebSocket-Version: 13
Sec-WebSocket-Key: b6gjhT32u488lpuRwKaOWs==
```

Если сервер может установить соединение WebSocket и соединение разрешено, сервер отправляет ответ об успешном установлении связи, на что указывает HTTP-код 101 Switching Protocols:
```shell
HTTP/1.1 101 Switching Protocols
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Accept: b6gjhT32u488lpuRwKaOWs=
```

После обновления соединения протокол переключается с HTTP на WebSocket, и хотя пакеты по-прежнему отправляются через TCP, связь теперь соответствует формату сообщений WebSocket.
Все данные могут быть фрагментированы, поэтому можно отправить огромное сообщение без предварительного объявления размера. В этом случае WebSockets разбивает его на фреймы. 
Каждый кадр содержит небольшой заголовок, который указывает длину и тип полезной нагрузки, а также является ли этот кадр последним.


## Frontend
Для начала нужно установить соединение с сервером с поддержкой WebSockets, а затем прослушивать сообщения как события JavaScript — так же, как вы прослушиваете генерируемые пользователем события.
В native JavaScript нужно создать объект WebSocket и добавить прослушивателей на события: 
* open(открытия)
* message(сообщения);
* close(закрытия). 
И использовать метод send для отправки данных на сервер.

```js
const socket = new WebSocket('ws://localhost:8080'); 
socket.addEventListener('open', (event) => { 
  socket.send('Hello Server!'); 
}); 

socket.addEventListener('message', (event) => { 
  console.log('Message from server ', event.data); 
});

socket.addEventListener('close', (event) => { 
  console.log('The connection has been closed'); 
});
```

## Backend
На сервере нужно прослушивать запросы WebSocket.
Воспользуемся популярным пакетом `ws` для открытия соединения и прослушивания сообщений:

```js
const WebSocket = require('ws');
const ws = new WebSocket.Server({ port: 8080 });

ws.on('connection', function connection(connect) {
  connect.on('message', function incoming(message) {
    console.log(`server received: ${message}`);
  });

  connect.send('got your message!');
});
```
В этом примере мы отправляем строки, распространенным вариантом использования WebSockets является отправка строковых данных JSON или даже двоичных данных,
что позволяет структурировать ваши сообщения в удобном для вас формате.
