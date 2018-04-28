# MySQL Queries 
echo "use sakila; select first_name, last_name from actor" | mysql -u root -p  > hw10.txt
use sakila;
DESCRIBE actor;
1a) select first_name, last_name from actor;
1b) select concat(first_name," " ,last_name) as 'Actor Name' from actor;
2a) select actor_id, first_name, last_name from actor where first_name= 'Joe';
2b) select actor_id, first_name, last_name from actor where last_name like '%GEN%';
2c) select actor_id, last_name, first_name from actor where last_name like '%LI%' order by last_name, first_name asc;
2d) select country_id, country from country where country in ('Afghanistan', 'Bangladesh', 'China');
3a) alter table actor add column middle_name varchar(50) after first_name;
3b) alter table actor modify middle_name blob;
3c) alter table actor drop column middle_name;
4a) select last_name,count(*) from actor GROUP BY last_name;
4b) select last_name,count(*) from actor GROUP BY last_name having count(*)>=2;
4c) UPDATE actor SET first_name='HARPO' WHERE first_name='GROUCHO';
4d) UPDATE actor SET first_name='MUCHO GROUCHO' WHERE first_name='HARPO';
5a) show create table address;
6a) select first_name, last_name, address from address inner join staff on address.address_id = staff.address_id;
6b) select sum(payment.amount) as total_amount,first_name, last_name from payment inner join staff on staff.staff_id=payment.staff_id group by payment.amount;
6c) select count(actor_id), film.title from film_actor inner join film on film_actor.film_id = film.film_id group by actor_id;
6d) select count(title) from film inner join inventory on film.film_id = inventory.film_id group by title having film.title ='Hunchback Impossible';
6e) select first_name, amount from (select sum(amount) as amount, first_name, min(last_name) as last_name from (select amount, first_name, last_name from payment inner join customer on payment.customer_id= customer.customer_id) as T group by first_name order by last_name asc) as P;
7a) select title from film where title in(select title from film where title like 'K%' OR  title like 'Q%') AND language_id=1;
7b) select actors from film_list where actors in (select actors from film_list where title= 'Alone Trip');
7c) select first_name, last_name, email from customer join customer_list on customer_id = ID where country= 'Canada';
7d) select title from film_list where  category='Family';
7e) select count(*) as cnt, title from inventory as i join rental as r join film_text as f on i.inventory_id=r.inventory_id AND f.film_id=i.film_id group by title order by cnt DESC;
7f) select store_id, sum(amount) as TotalBusiness from ( select store_id, amount from store left join payment on store.manager_staff_id = payment.staff_id) as T group by store_id;
7g) select * from storeLocation;
7h) select genre, sum(amount) as amount from
    (select amount, name as genre from
        (select amount, category_id from
            (select amount, film_id from
                (select  amount, inventory_id from payment
                    left join rental on payment.rental_id = rental.rental_id) as T1
                left join inventory on T1.inventory_id = inventory.inventory_id ) as T2
            left join film_category on T2.film_id = film_category.film_id) as T3
        left join category on T3.category_id = category.category_id) as T4
    group by genre
    order by amount desc limit 5;
8a) create view top_five_genres AS select store_id, city, country from store as s join staff_list as sl on sl.SID = s.store_id ;
8b) select * from top_five_genres ;
8c) drop view top_five_genres;

