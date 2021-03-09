# SpringBoot-Postgres templatization

## SpringBoot Initialzr
<p align="center">
  <img src="./images/Spring Initialzr missing JPA.png" width="900" height="500" title="Spring Initialzr">
</p>

## ```.mvn/wrapper``` directory => Run Your Maven Build Anywhere with the Maven Wrapper
## Where maven is downloaded from? => maven-wrapper.properties
<p align="center">
  <img src="./images//mvn directory.png" width="400" height="200" title="Spring Initialzr">
</p>

## Oooppss... forgot JPA (java Persistence API) => I could added it in the dependencies of my SpringBoot Initialzr
```
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
```

## Dependencies are located in the user's home directory inside the .m2 file

## Annotations 

#### @Entity =>  An entity represents a table stored in a database.

#### @Table => The easiest way to set a custom SQL table name is to annotate the entity

## HIghly used postgres commands 
```
postgres=> \l                 >>>      list all DBs

postgres=> \conninfo          >>>       "this gives me You are connected to database "?????" as user "????" via socket in "???" at port "????""

postgres=> \du                >>>       list of db users/accounts

                                   List of roles
 Role name |                         Attributes                         | Member of 
-----------+------------------------------------------------------------+-----------

```

# ```./mvnw spring-boot:run``` => the most important command in the SpringBoot application

# The least amount of code that a SpringBoot-Postgres Application will work

### Model File => NOTE: This code will just run but not create a table
### As a pre-requisite, you need the database created
```
@Entity
@Table(name = "sample")
public class Sample {

    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private Long id;

    private String sampleName;

    private Sample(String sampleName) {
      this.sampleName = sampleName;
    }

    public String getFirstName() {
       return firstName;
  }
}
```
### Thanks for zetocde for the sql scripts that are stored inside ```src/main/resources```
### schema.sql
```
DROP TABLE IF EXISTS sample;
CREATE TABLE sample (id serial PRIMARY KEY,
                    sampleName VARCHAR(255)
                    );
```
### data.sql
```
insert into sample (sampleName) values ('????');
insert into sample (sampleName) values ('????');
insert into sample (sampleName) values ('????');
```




