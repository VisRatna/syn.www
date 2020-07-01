# Blog

## Benchmarking MoodleBox on different Raspberry Pi models

Raspbian version : Raspbian GNU/Linux 10 (buster)

Moodle release : 3.8 (Build: 20191118)

MoodleBox version : 3.5.0 (2019-11-18)

MoodleBox plugin version : 2.4.2 (2019100700)

Kernel version : Linux 4.19.75-v7l armv7l

Moodle Benchmark plug-in version : v1.3.0 (2019083101)

SD card : SanDisk Ultra 16GB microSDHC I

\# | Item | Accpt. limit  | Crit. limit | RPi 3A+ | RPi 3B | RPi 3B+ | RPi 4B
:-:|-------------|--------------:|------------:|--------:|-------:|--------:|---:
1 | Moodle loading time | 0.5 | 0.8  | 0.020 | 0.022 | 0.024 | 0.025
2 | Processor processing speed | 0.5 |0.8 | 0.644 | 0.751 | 0.644 | 0.963
3 | Reading file performance | 0.5  | 0.8 | 0.045 | 0.051 | 0.044 | 0.046
4 | Writing file performance | 1.0 | 1.25 | 0.206 | 0.240 | 0.204 | 0.201
5 | Reading course performance | 0.75  | 1.0  | 0.114 | 0.147 | 0.127 | 0.077
6 | Writing course performance | 1.0 | 1.25 | 0.109 | 0.119 | 0.123 | 0.068
7 | Database performance (#1) | 0.5 | 0.7 | 0.021 | 0.025 | 0.025 | 0.015
8 | Database performance (#2) | 0.3 | 0.5 | 0.047 | 0.059 | 0.048 | 0.033
9 | Login time performance | 0.3 | 0.8 | 0.109 | 0.007 | 0.016 | 0.080
10 | Login time performance | 0.3 | 0.8 | 0.158 | 0.016 | 0.018 | 0.096
 | Total time | 5.65 | 6.7 | 1.473 | 1.437 | 1.273 | 1.628
 | Score (points)  | | | 148 | 144 | 128 | 161 

In all three cases the following warning was printed:

Watch out!
Your Moodle performance is not optimal.

The processor seems too slow.
Check that your hardware configuration is high enough to run Moodle.

\# | Item | Description
:-:|------------------------|-----------------------
1 | Moodle loading time | Load the "config.php" configuration file 
2 | Processor processing speed | Call a PHP function with a loop to check the processor speed 
3 | Reading file performance | Read a file multiple times to check the reading speed of the Moodle temporary folder 
4 | Writing file performance | Write a file multiple times to check the writing speed of the Moodle temporary folder 
5 | Reading course performance | Read a course multiple times to check the reading speed of the database 
6 | Writing course performance | Write a course multiple times to check the writing speed of the database
7 | Database performance (#1) | Run a complex SQL query to check the speed of the database
8 | Database performance (#2)|  Run a complex SQL query to check the speed of the database
9 | Login time performance | for the guest account Check the loading time of the guest account login page
10 | Login time performance | for a fake user account Check the loading time of a fake user account login page

(Last edited 2020-05-14 18:58 UTC)


## PHP and DBMS compatibility of major Moodle releases

In Moodle community forums we get a non-ending stream of requests from people having trouble in marching old Moodle installations to newer and supported realeases. Things break easily since along the line the system requirements have been evolving too. The following table summarizes their dependencies.

Release                                           | Earliest from | PHP min. | PHP max. | MySQL min. | MySQL max. | PgSQL min. | MariaDB min. | MariaDB max
------------------------------------------------- | ------------- | -------- | -------- | ---------- | ---------- | ---------- | ------------ | ---------
[1.6](https://docs.moodle.org/dev/Moodle_1.6_release_notes) <sup>[1]</sup> | 1.0 | 4.3.0    | 5.6      | 4.1.16     | ?          | 8.0        | - | -
[1.9](https://docs.moodle.org/dev/Moodle_1.9_release_notes) <sup>[2]</sup> | 1.6 | 4.3.0    | 5.6      | 4.1.16     | ?          | 8.0        | - | -
[2.2](https://docs.moodle.org/dev/Moodle_2.2_release_notes) <sup>[3]</sup> | 1.9 | 5.3.2    | 5.6      | 5.0.25     | ?          | 8.3        | - | -
[2.7](https://docs.moodle.org/dev/Moodle_2.7_release_notes) (LTS) | 2.2 | 5.4.4    | 5.6      | 5.5.31     | ?          | 9.1        | 5.5.31 | 10.2
[3.1](https://docs.moodle.org/dev/Moodle_3.1_release_notes) (LTS) | 2.7 | 5.4.4    | 7.0      | 5.5.31     | 5.7        | 9.1        | 5.5.31 | 10.2
[3.2](https://docs.moodle.org/dev/Moodle_3.2_release_notes)       | 2.7 | 5.6.5    | 7.1      | 5.5.31     | 5.7        | 9.1        | 5.5.31 | 10.2
[3.5](https://docs.moodle.org/dev/Moodle_3.5_release_notes) (LTS) | 3.1 | 7.0.0    | 7.2      | 5.5.31     | 8.0        | 9.3        | 5.5.31 | 10.5
[3.7](https://docs.moodle.org/dev/Moodle_3.7_release_notes)       | 3.2 | 7.1.0    | 7.3      | 5.6        | 8.0        | 9.4        | 10.0? | 10.5
[3.8](https://docs.moodle.org/dev/Moodle_3.8_release_notes)       | 3.2 | 7.1.0    | 7.3 <sup>[4]</sup> | 5.6        | 8.0        | 9.4        | 10.0? | 10.5
[3.9](https://docs.moodle.org/dev/Moodle_3.9_release_notes)&nbsp;(LTS)  | 3.5 | 7.2.0    | 7.4  | 5.6        | 8.0        | 9.4        | 10.2.29 | 10.5

1. Release 1.6 was a de-facto LTS, supported for 3 years

2. Release 1.9 was a de-facto LTS, supported for 6 years

3. Upgrade from 1.9 to 2.x broke so many things, it is advisable to rebuild the site - either through course backups and restore or create courses from scratch (making use of the numerous new features in Moodle 2 and 3).

4. PHP 7.4 since release 3.8.3

(Last edited 2020-06-27 08:30 UTC)
