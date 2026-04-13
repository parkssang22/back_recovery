```bash
SYS @ orcl > set lines 200 pages 9999
SYS @ orcl > Archive log list
Database log mode              Archive Mode
Automatic archival             Enabled
Archive destination            /home/oracle/arch4
Oldest online log sequence     33
Next log sequence to archive   36
Current log sequence           36
SYS @ orcl > select * from v$log;

    GROUP#    THREAD#  SEQUENCE#      BYTES  BLOCKSIZE    MEMBERS ARC STATUS           FIRST_CHANGE# FIRST_TIME       NEXT_CHANGE# NEXT_TIME               CON_ID
---------- ---------- ---------- ---------- ---------- ---------- --- ---------------- ------------- ------------------- ------------ ------------------- ----------
         1          1         33  209715200        512          2 YES INACTIVE               5540270 2026/04/13:14:15:14      5540752 2026/04/13:14:15:48       0
         2          1         34  209715200        512          2 YES INACTIVE               5540752 2026/04/13:14:15:48      5541327 2026/04/13:14:20:52       0
         3          1         35  209715200        512          2 YES ACTIVE                 5541327 2026/04/13:14:20:52      5542534 2026/04/13:14:46:38       0
         4          1         36  209715200        512          2 NO  CURRENT                5542534 2026/04/13:14:46:38   9.2954E+18                                   0

SYS @ orcl > alter system switch logfile;

System altered.

SYS @ orcl > Archive log list
Database log mode              Archive Mode
Automatic archival             Enabled
Archive destination            /home/oracle/arch4
Oldest online log sequence     34
Next log sequence to archive   37
Current log sequence           37
SYS @ orcl > select * from v$log;

    GROUP#    THREAD#  SEQUENCE#      BYTES  BLOCKSIZE    MEMBERS ARC STATUS           FIRST_CHANGE# FIRST_TIME       NEXT_CHANGE# NEXT_TIME               CON_ID
---------- ---------- ---------- ---------- ---------- ---------- --- ---------------- ------------- ------------------- ------------ ------------------- ----------
         1          1         37  209715200        512          2 NO  CURRENT                5542937 2026/04/13:14:48:22   9.2954E+18                                   0
         2          1         34  209715200        512          2 YES INACTIVE               5540752 2026/04/13:14:15:48      5541327 2026/04/13:14:20:52       0
         3          1         35  209715200        512          2 YES ACTIVE                 5541327 2026/04/13:14:20:52      5542534 2026/04/13:14:46:38       0
         4          1         36  209715200        512          2 YES ACTIVE                 5542534 2026/04/13:14:46:38      5542937 2026/04/13:14:48:22       0
```

## 오라클이 준비된 4개의 리두 로그 그룹을 한 바퀴 다 돌고 가장 처음에 썼던 1번 그룹을 성공적으로 재활용하기 시작한 것을 볼 수 있다
