# RAID

Source https://habr.com/ru/company/servermall/blog/304798/ , https://www.bestor.spb.ru/v3/faq?cat_id=87&subcat_id=85&faq_id=404

Чаще всего задачи, выполняемые серверами, требуют высокой скорости чтения/записи данных и/или необходимость сохранить данные при выходе из строя самих накопителей. Поэтому установка в сервер единственного диска редко имеет смысл. Этот вариант можно рассматривать, если нагрузка будет совсем небольшой, а сохранность данных не волнует вовсе. Да и объёмы информации, которыми оперируют серверы, часто требуют куда больше пространства для хранения, чем может дать один диск. А чем больше накопителей, тем выше вероятность выхода из строя, особенно при высокой нагрузке.

Проблемы производительности и отказоустойчивости дисковой подсистемы решаются с помощью создания массивов: логических структур, в которые с помощью RAID-контроллера объединяется несколько накопителей — жёстких дисков и SSD. При этом массив выглядит для системы единым пространством для хранения данных.

Существует много видов массивов, отличающихся производительностью, надёжностью хранения данных и минимально необходимым количеством дисков. Выбор конкретного вида зависит от ваших задач и потребностей, а также от возможностей самого RAID-контроллера.

### RAID контроллеры делятся на:

* **Программный**. Вся нагрузка по управлению массивом ложится на центральный процессор. Наименее производительное и отказоустойчивое решение.
* **Интегрированный**. Встроены в материнскую плату. Отдельный чип выполняет часть задач по управлению, но всё же тоже задействует центральный процессор. Интегрированные контроллеры могут иметь собственную кэш-память. По сравнению с программными, поддерживают больше видов массивов, работают куда быстрее и надёжнее.
* **Аппаратный**. Выполнены в виде плат расширений или отдельных устройств, размещённых вне сервера (внешние, или мостовые контроллеры). Оснащены собственным процессором, выполняющим все необходимые вычисления, и, как правило, кэш-памятью. Модульные контроллеры могут иметь внешние и внутренние порты:
  * Внутренние - предназначены для подключения накопителей, установленных в сам сервер.
  * Внешние — используются для подключения внешних дисковых хранилищ.


### Чтобы при сбое питания не потерять данные, находящиеся в кэше, используется два разных подхода:

* контроллер оснащается собственной батарейкой (BBU — Battery Backup Unit), позволяющей хранить данные в памяти до 3 суток,
* либо дополнительной флэш-памятью, питаемой от ёмкого конденсатора. При сбое питания в неё выгружает содержимое кэша. А поскольку флэш-память потребляет очень мало энергии, то и данные в ней сохраняются месяцами. Обратите внимание, что флэш-память используется только при сбое питания

**Write Through и Write Back** - способ записи данных, полученных RAID контроллером, на дисковый массив. По другому эти способы еще называются так: прямая запись (Write Through) и отложенная запись (Write Back). Какой из этих способов будет использоваться определяется в BIOS-е контроллера (либо при создании массива, либо позднее).

* **Write Through** - данные записываются непосредственно на дисковый массив. Т.е. как только данные получены, они сразу же записываются на диски и после этого контроллер подает сигнал управляющей ОС о завершении операции.
* **Write Back** - данные записываются сначала в кэш, и только потом (либо по мере заполнения кэш-а, либо в моменты минимальной загрузки дисковой системы) из кэш-а на диски. При этом, сигнал о завершении операции записи передается управляющей ОС сразу же по получении данных кэш-ем контроллера.

Write Back работает быстрее, но при этом надо помнить, что в случае сбоя питания все данные, которые находились в этот момент в кэш-е, будут потеряны. Причем, управляющая ОС (а следовательно и приложение, записывавшее эти данные) ничего об этом "не узнают", так как они уже получили сообщение от контроллера об успешном завершении записи. Например, если в кэше находились данные транзакции сервера СУБД, то СУБД будет уверенна, что с данными все хорошо, хотя на самом деле это не так.

### BBU

**BBU (Battery Backup Unit)** необходим для предотвращения потери данных находящихся в кэш-е RAID контроллера и еще не записанных на диск (отложенная запись - "write-back caching"), в случае аварийного выключения компьютерной системы.

Существуют три разновидности BBU:

* Просто BBU: это аккумулятор, который обеспечивает резервное питание кэша через RAID контроллер.
* Переносимые (Transportable) BBU (tBBU): это аккумулятор, который размещен непосредственно на модуле кэш и питает его независимо от RAID контроллера. В случае выхода из строя RAID контроллера, это позволяет перенести данные, сохраненные в кэш-е, на резервный контроллер и уже на нем завершить операцию записи данных.
* Flash BBU: основная идея заключается в следующем: в случае сбоя питания RAID контроллер копирует содержимое кэш-а в энергонезависимую память (например, в случае с технологией Adaptec » Zero-Maintenance Cache Protection - на NAND флэш накопитель). Питание, необходимое для завершения этого процесса, обеспечивается встроенным супер-конденсатором. После восстановления питания, данные из флэш памяти копируются обратно в кэш контроллера.

### **Hotswap** - Hot Replacement of Disks / Hot Swap (Горячая Перестановка / Горячая Замена Дисководов) - это возможность замены вышедших из строя дисководов без прерывания работы системы. Если в системе используется должным образом сконфигурированный RAID контроллер, управляющий избыточной дисковой системой (RAID массивом), то отказ одного дисковода не приводит к прерыванию функционирования системы. В этом случае системой генерируется соответствующее сообщение для системного оператора. Через некоторое время, когда активизируется замещающий дисковод, системный оператор может удалить отказавший дисковод, установить новый дисковод, и дать контроллеру команду "восстановить" данные на новом дисководе, причем все это происходит без прерывания системных операций и выключения системы.

### **Hot Spare** 

Hot Spare- (Резервная Замена Дисководов ("Горячее резервирование")) - Одна из наиболее важных особенностей, которую обеспечивает RAID контроллер, с целью достичь безостановочное обслуживание с высокой степенью отказоустойчивости. В случае выхода из строя диска, восстанавливающая операция будет выполнена RAID контроллером автоматически, если выполняются оба из следующих условий:

1. Имеется "резервный" диск идентичного объема, подключенный к тому же контроллеру и назначенный в качестве резервного, именно он и называется Hotspare ;
1. Отказавший диск входит в состав избыточной дисковой системы, например RAID 1, RAID 3, RAID 5 или RAID 0+1.

Обратите внимание: резервирование позволяет восстановить данные, находившиеся на неисправном диске, если все диски подключены к одному и тому же RAID контроллеру.
"Резервный" диск может быть создан одним из двух способов:

1. Когда пользователь выполняет утилиту разметки, все диски, которые подключены к контроллеру, но не сконфигурированы в любую из групп дисководов, будут автоматически помечены как "резервные" ( Hotspare ) диски (автоматический способ поддерживается далеко не всеми контроллерами).
1. Диск может также быть помечен как резервный ( Hotspare ), при помощи соответствующей утилиты RAID контроллера.
В течение процесса автоматического восстановления система продолжает нормально функционировать, однако производительность системы может слегка ухудшиться.

Для того, что бы использовать восстанавливающую особенность резервирования, Вы должны всегда иметь резервный диск ( Hotspare ) в вашей системе. В случае сбоя дисковода, резервный дисковод автоматически заменит неисправный диск, и данные будут восстановлены. После этого, системный администратор может отключить и удалить неисправный диск, заменить его новым диском и сделать этот новый диск резервным.

### **CopyBack Hot Spare**

Source https://internet-lab.ru/copyback_hot_spare

Copyback Hot Spare — это функция RAID контроллера, которая позволяет закрепить физическое расположение диска "горячего резерва" (Hot Spare), что позволяет улучшить управляемость системы.

Т.е. произошло следующее:

1. Сдох диск в слоте №1.
  * RAID контроллер исключил дохлый диск из массива.
  * RAID контроллер использовал вместо неисправного диска HOT SPARE из слота №11.
 
2. Дохлый диск в слоте №1 был заменён на исправный.
  * RAID контроллер увидел новый диск в слоте №1, установил ему статус Replacing (Copyback) и начал перекачивать на него данные с диска в слоте №11.
  * После окончания процедуры RAID контроллер должен ввести в массив диск в слоте №1, а диск в слоте №11 выкинуть из массива и сделать HOT SPARE.

#### JBOD 

JBOD(Just a Bunch of Disks) это способ подключить диски к RAID контроллеру не создавая на них никакого RAID. Каждый из дисков доступен так же, как если бы он был подключен к обычному адаптеру. Эта конфигурация применяется когда необходимо иметь несколько независимых дисков, но не обеспечивает ни повышения скорости, ни отказоустойчивости.

#### Stripe size
Размер страйпа (stripe size) определяет объем данных записываемых за одну операцию ввода/вывода. размер страйпа задается в момент конфигурирования RAID массива и не может быть изменен позднее без переинициализации всего массива. Больший размер страйпа обеспечивает прирост производительности при работе с большими последовательными файлами (например, видео), меньший - обеспечивает большую эффективность в случае работы с большим количеством небольших файлов.
