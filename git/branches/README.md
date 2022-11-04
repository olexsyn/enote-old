# Робота з гілками

- Галуження в git
  - [Гілки у кількох словах](https://git-scm.com/book/uk/v2/%D0%93%D0%B0%D0%BB%D1%83%D0%B6%D0%B5%D0%BD%D0%BD%D1%8F-%D0%B2-git-%D0%93%D1%96%D0%BB%D0%BA%D0%B8-%D1%83-%D0%BA%D1%96%D0%BB%D1%8C%D0%BA%D0%BE%D1%85-%D1%81%D0%BB%D0%BE%D0%B2%D0%B0%D1%85) :link:
  - [Основи галуження та зливання](https://git-scm.com/book/uk/v2/%D0%93%D0%B0%D0%BB%D1%83%D0%B6%D0%B5%D0%BD%D0%BD%D1%8F-%D0%B2-git-%D0%9E%D1%81%D0%BD%D0%BE%D0%B2%D0%B8-%D0%B3%D0%B0%D0%BB%D1%83%D0%B6%D0%B5%D0%BD%D0%BD%D1%8F-%D1%82%D0%B0-%D0%B7%D0%BB%D0%B8%D0%B2%D0%B0%D0%BD%D0%BD%D1%8F) :link:
  - [Управління гілками](https://git-scm.com/book/uk/v2/%D0%93%D0%B0%D0%BB%D1%83%D0%B6%D0%B5%D0%BD%D0%BD%D1%8F-%D0%B2-git-%D0%A3%D0%BF%D1%80%D0%B0%D0%B2%D0%BB%D1%96%D0%BD%D0%BD%D1%8F-%D0%B3%D1%96%D0%BB%D0%BA%D0%B0%D0%BC%D0%B8) :link:
  - [Процеси роботи з гілками](https://git-scm.com/book/uk/v2/%D0%93%D0%B0%D0%BB%D1%83%D0%B6%D0%B5%D0%BD%D0%BD%D1%8F-%D0%B2-git-%D0%9F%D1%80%D0%BE%D1%86%D0%B5%D1%81%D0%B8-%D1%80%D0%BE%D0%B1%D0%BE%D1%82%D0%B8-%D0%B7-%D0%B3%D1%96%D0%BB%D0%BA%D0%B0%D0%BC%D0%B8) :link:
  - [Віддалені гілки](https://git-scm.com/book/uk/v2/%D0%93%D0%B0%D0%BB%D1%83%D0%B6%D0%B5%D0%BD%D0%BD%D1%8F-%D0%B2-git-%D0%92%D1%96%D0%B4%D0%B4%D0%B0%D0%BB%D0%B5%D0%BD%D1%96-%D0%B3%D1%96%D0%BB%D0%BA%D0%B8) :link:
  - [Перебазовування](https://git-scm.com/book/uk/v2/%D0%93%D0%B0%D0%BB%D1%83%D0%B6%D0%B5%D0%BD%D0%BD%D1%8F-%D0%B2-git-%D0%9F%D0%B5%D1%80%D0%B5%D0%B1%D0%B0%D0%B7%D0%BE%D0%B2%D1%83%D0%B2%D0%B0%D0%BD%D0%BD%D1%8F) :link:

([git-scm.com/book](https://git-scm.com/book/uk/v2/) :link:)

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


