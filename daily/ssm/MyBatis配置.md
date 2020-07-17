# MyBatis入门

## mapper接收参数

1. 普通参数

    ```xml
    <select id="selectUser" resultType="int">
      select id, username, password
      from users
      where id = #{id}
    </select>
    ```

    parameterType可以不指定，也可以指定类型

2. 传入bean对象

    ```xml
    <insert id="insertUser" parameterType="com.example.User">
      insert into users (id, username, password)
      values (#{id}, #{username}, #{password})
    </insert>
    ```

    parameterType指定bean的全限定类名，在使用到的参数会从bean中查找

3. 