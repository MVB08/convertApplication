# JavaExam
Консольная утилита для скачивания файлов по HTTP протоколу.


Входные параметры:

n количество одновременно качающих потоков (1,2,3,4....)
f путь к файлу со списком ссылок
o имя папки, куда складывать скачанные файлы


Пример вызова:

java -jar utility.jar 5 output_folder links.txt


Формат файла со ссылками:

<HTTP ссылка><пробел><имя файла, под которым его надо сохранить>


Пример:


http://example.com/archive.zip my_archive.zip

http://example.com/image.jpg picture.jpg
......


В HTTP ссылке нет пробелов, нет encoded символов и прочей ерунды — 
это всегда обычные ссылки с английскими символами без специальных символов в именах файлов и прочее. 
Короче — ссылкам можно не делать decode. 
Ссылки без авторизации, не HTTPS/FTP — всегда только HTTP-протокол.


Ссылки могут повторяться в файле, но с разными именами для сохранения, например:

http://example.com/archive.zip first_archive.zip

http://example.com/archive.zip second_archive.zip


Одинаковые ссылки — это нормальная ситуация, ее необходимо учитывать. 
То есть, нет смысла загружать одно и тоже дважды, особенно если речь идет о гигабайтах.
Подразумевается, что один поток качает один файл, не надо качать один файл в несколько потоков. 
То есть если файлов 2, а потоков 3, то надо запустить два потока, каждый из которых будет загружать один файл.


Выходные данные:

Все файлы загружаются в n потоков.
В процессе работы утилита должна выводить статистику — время работы и количество скачанных байт виде:


Загружается файл: %ИМЯ%

Файл %ИМЯ% загружен: 1 MB за 1 минуту


После завершения работы программа выводит:


Завершено: 100%
Загружено: 17 файлов, 2.3 MB
Время: 2 минуты 13 секунд
Средняя скорость: 17.2 kB/s


Утилита должна быть написана на Java (версия 7 или выше). 