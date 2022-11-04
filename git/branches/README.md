# Робота з гілками

[Галуження в git](https://git-scm.com/book/uk/v2/%D0%93%D0%B0%D0%BB%D1%83%D0%B6%D0%B5%D0%BD%D0%BD%D1%8F-%D0%B2-git-%D0%9E%D1%81%D0%BD%D0%BE%D0%B2%D0%B8-%D0%B3%D0%B0%D0%BB%D1%83%D0%B6%D0%B5%D0%BD%D0%BD%D1%8F-%D1%82%D0%B0-%D0%B7%D0%BB%D0%B8%D0%B2%D0%B0%D0%BD%D0%BD%D1%8F) :link:

Створити нову гілку 'iss53' і перейти в неї

    $ git branch iss53
    $ git checkout iss53

Або скорочено:

    $ git checkout -b iss53
    Switched to a new branch "iss53"

Міняємо файли...  
Коммітимо:

    $ git commit -a -m 'added chahges for [issue 53]'

Коли робота закінчена і перевірена працездатність, перемикаємося на основну гілку і зливаемо зміни:

    $ git checkout main
    Switched to branch 'main'
    $ git merge iss53

Якщо гілка 'iss53' більше не потрібна - видаляємо її.

    $ git branch -d iss53

[git-scm.com/book](https://git-scm.com/book/uk/v2/%D0%93%D0%B0%D0%BB%D1%83%D0%B6%D0%B5%D0%BD%D0%BD%D1%8F-%D0%B2-git-%D0%9E%D1%81%D0%BD%D0%BE%D0%B2%D0%B8-%D0%B3%D0%B0%D0%BB%D1%83%D0%B6%D0%B5%D0%BD%D0%BD%D1%8F-%D1%82%D0%B0-%D0%B7%D0%BB%D0%B8%D0%B2%D0%B0%D0%BD%D0%BD%D1%8F)
