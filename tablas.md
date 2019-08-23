## Tablas

```sql
drop table heroes;

create table heroes(
idHero int,
name varchar(400),
superpower varchar(400)
);

insert into heroes values (1, 'Iron man', 'traje poderoso');
insert into heroes values (2, 'Spiderman man', 'sentidos arácnidos');
insert into heroes values (3, 'Capitan América', 'escudo y fuerza');
insert into heroes values (4, 'Hulk', 'super fuerza');
insert into heroes values (5, 'Capitan Marvel', 'super poderosa');

drop table preAvengers;

create table preAvengers(
name varchar(100),
email  varchar(100),
welcome int
);

drop table avengers;

create table avengers(
idAvenger int IDENTITY(1,1) PRIMARY KEY,
name varchar(100),
email  varchar(100),
welcome int
);

drop table missions;
create table missions(
avenger int,
hero int
);
```
