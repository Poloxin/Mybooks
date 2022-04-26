# Authentification (PKI)

**PKI (public key infrastructure)** - это набор различных технологий, которые используются для обеспечения аутентификации источника, целостности данных и конфиденциальности для пользователя в сети. PKI использует преимущества асимметричного шифрования и использует пары открытого и закрытого ключей для шифрования данных.

Центр Сертификации (CA - Certificate Authority)

Центр сертификации создаёт сертификат своим закрытым ключём, в сертификате находится электронная подпись сервера, если получается расшифровать открытм ключём и он такой же как в сертификате, значет можно доверять.

###### Важное примечание! Цифровой сертификат создается при объединении ключа и цифровой подписи. Сертификат будет содержать сведения о владельце сертификата, например, об организации.

ЦС выдаст объекту цифровой сертификат только после того, как его личность будет проверена. После того, как ЦС создает цифровой сертификат, он сохраняется в базе данных сертификатов, которая используется для безопасного хранения всех утвержденных ЦС цифровых сертификатов.

Цифровой сертификат форматируется с использованием стандарта X.509, который содержит следующие сведения:

- Номер версии

- Серийный номер

- Идентификатор алгоритма подписи

- Название эмитента

- Срок годности

- Не раньше, чем

- Не после

- Имя субъекта

- Информация об открытом ключе субъекта

- Алгоритм открытого ключа

- Открытый ключ субъекта

- Уникальный идентификатор эмитента (необязательно)

- Уникальный идентификатор субъекта (необязательно)

- Расширения (необязательно)

- Алгоритм подписи сертификата

- Подпись сертификата

- Регистрирующий орган (RA)

###### Важное примечание! Цифровой сертификат создается при объединении ключа и цифровой подписи. Сертификат будет содержать сведения о владельце сертификата, например, об организации.

### Электронная подпись

Процесс создания:

1. Будет использовать алгоритм хеширования для создания хэша (дайджеста) сообщения

2. Затем будет использовать закрытый ключ для шифрования хэша (дайджеста) сообщения


Цифровые подписи используются не только для проверки подлинности сообщений. Они также используются в следующих случаях:

- Цифровые подписи для цифровых сертификатов: это позволяет отправителю вставить цифровую подпись в цифровой сертификат.
- Цифровые подписи для подписи кода: это позволяет разработчику приложения вставить свою цифровую подпись в исходник приложения, чтобы помочь пользователям проверить подлинность программного обеспечения или приложения.