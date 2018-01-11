How mybatis recognize a paramater in the DAO interface?

```xml
<select id="queryAll" resultType="Seckill">
      SELECT seckill_id, name, number, start_time, end_time, create_time
      FROM seckill
      ORDER BY create_time DESC
      LIMIT #{offset}, #{limit}
    </select>
```

```java
List<Seckill> queryAll(@Param("offset") int offset, @Param("limit") int limit);
```
Use the @Param() annotation to assign the parameter name for a parameter. Otherwise, Java will convert int offset to arg0, and so on.

If there is only one parameter in the function, then any name can be used in the xml #{} to refer to the parameter.
