1. Скачал [Kali](https://www.kali.org/get-kali/#kali-virtual-machines) для VMware
2. Запустил Kali (kali/kali)
3. Установил [AFLplusplus](https://github.com/AFLplusplus)
   1. Установил Docker ![img1](./img/docker1.png)
   2. Запустил Docker ![img2](./img/docker2.png)
   3. Скачал образ AFLplusplus ![img3](./img/docker3.png)
   4. Запустил образ AFLplusplus ![img4](./img/docker4.png)
4. Начал работать с AFLplusplus 
   1. Начал тестировать [wisdom-alt](https://github.com/KarenWest/softwareSecurity/blob/master/wisdom-alt.c)
      1. Скомпилировал `wisdom-alt.c` с помощью специального компилятора `afl-cc` ![img5](./img/afl1.png)
      2. Создал специальный файлик с валидными входными параметрами ![img6](./img/afl2.png)
      3. Запустил `fuzzинг` ![img7](./img/afl3.png)
      4. Подождал какое то время и остановил тестирование ![img8](./img/afl4.png)
      5. Проверил результаты `crachей` ![img9](./img/afl5.png)
   2. Начал тестировать [proftp](http://www.proftpd.org)
      1. Скачал "правильную" версию `proftp` с помощью `wget ftp://ftp.proftpd.org/distrib/source/proftpd-1.3.5.tar.gz` ![img10](./img/afl6.png)
      2. Распаковал ![img11](./img/afl7.png)
      3. Собрал 1/3 ![img12](./img/afl8.png)
      4. Собрал 2/3 ![img13](./img/afl9.png)
      5. Собрал 3/3 ![img14](./img/afl10.png)
      6. Запустил с помощью `./proftpd -n` ![img15](./img/afl11.png)
      7. ...
      8. ... ...
      9. ... ... ...
      10. ... ... ... ...
      11. ... ... ... ... ...
5. Собрал отчет
   1. Формочка-текст такой же как этот список
   2. Фотографии в папке `img`
   3. Пример вывода фазинга для каждого кода в соответствующей папке в `code`