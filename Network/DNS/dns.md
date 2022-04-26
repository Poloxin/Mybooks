# DNS basic

- [Why use UDP](://stackoverflow.com/questions/40063374/why-dns-uses-udp-as-the-transport-layer-protocol/40063433#40063433)

	- UDP is much faster. TCP is slow as it requires 3 way handshake. The load on DNS servers is also an important factor. DNS servers (since they use UDP) don’t have to keep connections.
	- DNS requests are generally very small and fit well within UDP segments.
	- UDP is not reliable, but reliability can be added on application layer. An application can use UDP and can be reliable by using timeout and resend at application layer.

- [Format of DNS request](https://habr.com/ru/post/346098/)

- [Recursive and non-recursive](https://ru.stackoverflow.com/questions/314833/dns-%D1%81%D0%B5%D1%80%D0%B2%D0%B5%D1%80%D0%B0-%D1%80%D0%B5%D0%BA%D1%83%D1%80%D1%81%D0%B8%D0%B2%D0%BD%D1%8B%D0%B9-%D0%B7%D0%B0%D0%BF%D1%80%D0%BE%D1%81-%D0%B8-%D0%BD%D0%B5%D1%80%D0%B5%D0%BA%D1%83%D1%80%D1%81%D0%B8%D0%B2%D0%BD%D1%8B%D0%B9)

При рекурсивном запросе Вы просто обращаетесь к серверу, а он, если не найдет у себя нужной записи, идет к другим серверам и спрашивает у них. Нерекурсивный dns сервер в данном случае просто говорит - "я не знаю, но спроси у этого сервера". И клиент будет слать ещё один запрос. Понятное дело, что при медленном интернете первый вариант лучше.

Bind, классический dns сервер поддерживает оба варианта и позволяет их тонко настраивать.


