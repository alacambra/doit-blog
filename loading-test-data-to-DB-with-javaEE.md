In the persistence.xml file, it is possible to use the property <code>javax.persistence.sql-load-script-source</code>

This property allows you to populate your datasource with given data. 
The value is just a sql script file containing the insert statements to be used. 
```xml
<property name="javax.persistence.sql-load-script-source" value="META-INF/test-data.sql"/>
```

Analogous, you can also use properties to drop data. Many other options are available. If you are interested, just take a look at  the section *9.4 Schema Generation*	from [*JSR-000338 JavaTM Persistence 2.1*](http://download.oracle.com/otndocs/jcp/persistence-2_1-fr-eval-spec/index.html)

My persistence.xml file is like follows:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<persistence version="2.1" xmlns="http://xmlns.jcp.org/xml/ns/persistence" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/persistence http://xmlns.jcp.org/xml/ns/persistence/persistence_2_1.xsd">
<persistence-unit name="Cookinghelper" transaction-type="JTA">
    <jta-data-source>java:jboss/datasources/cookinghelper</jta-data-source>
    <exclude-unlisted-classes>false</exclude-unlisted-classes>
    <properties>
        <property name="hibernate.show_sql" value = "false" />
        <property name="javax.persistence.schema-generation.database.action" value="drop-and-create"/>
        <property name="javax.persistence.sql-load-script-source" value="META-INF/test-data.sql"/>
    </properties>
</persistence-unit>
</persistence>
</code>
```