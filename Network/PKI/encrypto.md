# Encryption

Два типа шифрования: 

- Симетричное - один общий ключ. Не безопасное, но очень быстрое. Длина ключа от 40 до 256 бит. Оба участника до начала обмена информацией должны знать ключ **Pre-Shared Key (PSK)**. Шифруют либо блочно, либо потоково
	
	- Блочное шифрование - блоки по 64-бита или 128-бит

	- Потоковое шифрование - побитное шифрование

		- AES (Advanced Encryption Standart). Использует ключи размером 128, 192 и 256 бит. Шифрование блоков 128, 192 и 256 бит. Считается боллее безопасным нежели DES 3DES. SSH v2 использует AES по defaultу.

		- DES (Data Encryption Algorithm). Старый алгоритм, шифрует блоками по 64 бита и ключ 54 бита.

		- 3DES (Triple Data Encryption Algorithm). Три раза подряд зашифровывает данныеi поблочно. Использует ключи размером 112 бит и 168 бит.

		- Software-Optimized Enctyption Algorithm (SEAL). Алгоритм потокового шифрования, который использует ключ размером 160 бит.

		- RC4, RC5, RC6 (Rivest cipher). Потоковый алогоритм шифрования, использующий размер ключа 256 бит.

- Ассиметричное - два ключа(открытый, закрытый) расшифровывают друг друга. Безопасное, но очень медленное. Размер ключа от 512 до 4096 бит. Однако рекомендуемый размер ключа в 1024 бита или более.

	- Сетевые протоколы: ssh, ssl, ike, pgp.

		- ElGamal - алгаритм основан на процессе согласования ключей DH. Принимает входной текст и преобразует в зашифрованный, который будет в два раза больше оригинала.

		- RSA (Rivest-Shamir-Adleman). Размер ключа от 512 до 2048 бит.

		- DSA (Digital Signature Algorithm), DSS (Digital Signature Standart). Алгоритм для цифровых подписей. Размеры ключей от 512 до 1024 бит.

		- Diffie-Hellman. Не является алгоритмом шифрования данных, а используется для безопасной доставки пар ключей по незащищённой сети. Использует ключи размером 512 бит, 1024 бит, 2048, 3078 и 4096 бит.
			
			- Diffie-Hellman group размер ключей:

				- DH 1 : 768 бит

				- DH 2 : 1024 бит

				- DH 5 : 1536 бит 

				- DH 14 : 2048 бит 

				- DH 15 : 3078 бит 

				- DH 16 : 4096 бит 

- Гибридное шифрование - компромисс между семетрией и ассиметрией. Сначало ассиметрия для передачи симетричного ключа, потом юзают симетрия.
