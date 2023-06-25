# liquibase
Liquibase se utiliza como una solucion a la administracion de bases de datos de `codigo abierto` que nos permite realizar facilmente las revisiones y cambios en nuestras bases de datos

* Elimine errores y retrasos al liberar bases de datos.
* Implemente y revierta los cambios para versiones específicas sin necesidad de saber lo que ya se ha implementado.
* Implemente los cambios de la base de datos y la aplicación juntos para que siempre estén sincronizados.

### URL EJEMPLOS LIQUIBASE

Los ejemplos de estructura `CHANGE TYPE` se encuentran en la documentacion dentro de la pagina oficial de Liquibase.
aca podras encontrar mas ejemplos desde creacion de tablas, update, primary key etc.

```url 
https://docs.liquibase.com/change-types/home.html
```


###### @CREAR PROYECTO LIQUIBASE SPRING BOOT:

![Image text](https://github.com/dev-rech/images/blob/master/liquibase_spring.png)

En los properties del proyecto se debe agregar lo siguiente:
```properties
spring.datasource.url=jdbc:h2:~/liquibase;DB_CLOSE_ON_EXIT=FALSE
spring.datasource.username=${USER_DATABASE}
spring.datasource.password=${USER_PASSWORD}
### Se debe especificar la ruta del archivo  changelog
spring.liquibase.change-log=classpath:db/changelog/db.changelog-master.xml
```

Agregar lo siguiente al archivo db.changelog-master.yaml.

En este caso ocuparemos `yaml` pero Liquibase admite los siguientes formatos: 
* XML
```xml
<changeSet  author="liquibase-docs"  id="createTable-example">
    <createTable catalogName="department"
                 remarks="A String"
                 schemaName="public"
                 tableName="person"
                 tablespace="A String">
        <column  name="address"  type="varchar(255)"/>
    </createTable>
</changeSet>
```
* YAML
```yaml
-  changeSet:
     id:  createTable-example
     author:  liquibase-docs
     changes:
       -  createTable:
            catalogName:  department
            columns:
              -  column:
                   name:  address
                   type:  varchar(255)
            remarks:  A String
            schemaName:  public
            tableName:  person
            tablespace:  A String
```
* JSON
```json
{
  "changeSet": {
    "id": "createTable-example",
    "author": "liquibase-docs",
    "changes": [
      {
        "createTable": {
          "catalogName": "department",
          "columns": [
            {
              "column": {
                "name": "address",
                "type": "varchar(255)"
              }
            }
          ],
          "remarks": "A String",
          "schemaName": "public",
          "tableName": "person",
          "tablespace": "A String"
        }
      }
    ]
  }
}
```
* SQL
```sql
CREATE  TABLE  department.person  (address  VARCHAR(255)  NULL)  COMMENT='A String';
ALTER  TABLE  department.person  COMMENT  =  'A String';
```
Escoge el lenguaje que mas te acomode