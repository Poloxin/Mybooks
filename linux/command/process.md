# Process

- `PID` - process id

- `ps` - process state. Display info about active processes

|State|Value                                                                                                   |
|-----|--------------------------------------------------------------------------------------------------------|
|R    |Progress or ready for progress                                                                          |
|S    |Stoped. Probably it waiting an action or net packet                                                     |
|D    |Stoped without opportunities of interrupts(прерывания). Probably it wait input/output maybe disk dev    |
|T    |Stoped. Process forcibly stoped(принудительно)                                                          |
|Z    |Zombi-process, not action,dautcher process that ended but paren process did't kill this                 |
|<    |Hige priority process. No niceness process, can get more time of processor work                         |
|N    |Low priority process. Niceless process, wait while hige priority process get time of processor work     |

- `aux` - more info

- `top` - show process info in real time

|String|Place        |Value                                                                            |
|------|-------------|---------------------------------------------------------------------------------|
|1     |top          |Name of programm                                                                 |
|      |14:29:20     |Current Time                                                                     |
|      |up 6:30      |Uptime                                                                           |
|      |2 users      |Two users work now                                                               |
|      |load average:|Three parametrs, first : 60 sec average, second: 5 min average, 15 min of average|
|2     |tasks:       |Summory of all process                                                           |
|      |2,3 us       |Percent of processor time on users tasks, no core tasks                          |
|      |0,7 sy       |Percent of processor time on system tasks,core                                   |
|      |0,0 ni       |Percent of processor time on nice (уступчивые, низкоприоритетные) process        |
|      |1,2 id       |Percent of processor time on downtime (простои)                                  |
|3     |Mem:         |Use of memory                                                                    |
|4     |Swap:        |Use virtual mem                                                                  |


## Manage of process

**Execute programm in the background with symbol `&`**

xlogo &

**Output of background play programm:**

[number] PID

Number of task and PID

- `jobs` - tasks запущенных в терминале

- `fg %number of task` - return program to front

- `bg %number of task` - return program to back

- `kill [-sigan] PID` - send signal to programm 

- `killall -u username [-signal] PID or name` - kill several process
