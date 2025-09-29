MyBatis 是一款优秀的持久层框架

它支持自定义 SQL、存储过程以及高级映射。

MyBatis 免除了几乎所有的 JDBC 代码以及设置参数和获取结果集的工作。

MyBatis 可以通过简单的 XML 或注解来配置和映射原始类型、接口和 Java POJO（Plain Old Java Objects，普通老式 Java 对象）为数据库中的记录。

## 从maven仓库使用
```xml
<dependency>
    <groupId>org.mybatis</groupId>
    <artifactId>mybatis</artifactId>
    <version>3.5.2</version>
</dependency>
```
## 持久层
完成持久化工作的代码块

持久化就是将程序的数据在持久状态和瞬时状态转化的过程
## mybatis 优点
- 帮助程序员将数据存入到数据库中
- 方便
- jdbc过于复杂，简化框架。
- 实现自动化
- 不使用框架也能写网站，但是使用框架更容易上手
- 优点
  - 简单易学
  - 灵活
  - sql和代码的分离，提高代码的可维护性
  - 提供映射标签，支持对象关系组件维护
  - 提供xml标签，支持编写动态sql

# mybatis程序
## 搭建环境
搭建数据库
新建maven项目,导入maven依赖
```xml
 <dependencies>
<!--        mysql驱动-->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>8.0.28</version>
        </dependency>
<!--        junit-->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.11</version>
            <scope>test</scope>
        </dependency>
<!--        mybatis-->
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>3.5.2</version>
        </dependency>
    </dependencies>
```
## 创建模块
创建mybatis的核心配置文件
```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "https://mybatis.org/dtd/mybatis-3-config.dtd">
<!--configuration核心配置文件-->
<configuration>
    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.cj.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql://localhost:3306/mybatis?useSSL=true&amp;useUnicode=true&amp;characterEncoding=UTF-8"/>
                <property name="username" value="root"/>
                <property name="password" value="root"/>
            </dataSource>
        </environment>
    </environments>
</configuration>
```
编写mybatis工具类
```java
// SqlSessionFactory--> SqlSession
public class MybatisUntils {
    private static SqlSessionFactory sqlSessionFactory;
    static {
        try {
            //获取 SqlSessionFactory对象
            String resource = "org/mybatis/example/mybatis-config.xml";
            InputStream inputStream = Resources.getResourceAsStream(resource);
            sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
    //既然有了 SqlSessionFactory，顾名思义，我们可以从中获得 SqlSession 的实例。
    // SqlSession 提供了在数据库执行 SQL 命令所需的所有方法。
    public static SqlSession getSqlSession(){
        return sqlSessionFactory.openSession();
    }
}

```


# mybatis 高级映射
核心概念：resultMap

基础： <resultMap> 是 MyBatis 映射配置的灵魂。它定义了如何将数据库查询结果集（ResultSet）中的列映射到 Java 对象（或嵌套对象）的属性上。

对比 resultType：
resultType：直接指定一个简单 Java 类型（如 String, Integer）或一个 POJO 类。MyBatis 会尝试根据列名自动映射到 POJO 的同名属性上（开启 autoMappingBehavior 时）。适合简单查询。

resultMap：显式定义映射规则，提供最大的灵活性。可以处理复杂的嵌套对象、集合、关联关系、类型转换、构造函数映射等。高级映射必用 resultMap。
## 一对一关联 (<association>)
场景： 一个对象“拥有”另一个对象。
实现 嵌套结果映射 (Nested Result Map - 推荐)： 使用单条 SQL JOIN 语句查询所有数据，MyBatis 根据结果映射规则组装嵌套对象。
```xml
<resultMap id="orderWithCustomerMap" type="Order">
    <id property="id" column="order_id"/>
    <result property="orderNumber" column="order_number"/>
    <!-- 其他 Order 属性映射 -->
    <association property="customer" javaType="Customer">
        <id property="id" column="customer_id"/>
        <result property="name" column="customer_name"/>
        <result property="email" column="customer_email"/>
        <!-- 其他 Customer 属性映射 -->
    </association>
</resultMap>
<select id="selectOrderWithCustomer" resultMap="orderWithCustomerMap">
    SELECT
        o.id AS order_id,
        o.order_number,
        c.id AS customer_id,
        c.name AS customer_name,
        c.email AS customer_email
    FROM orders o
    INNER JOIN customers c ON o.customer_id = c.id
    WHERE o.id = #{id}
</select>
```
## 一对多关联 (<collection>)
场景： 一个对象“拥有”一个其他对象的集合。例如：Order 拥有多个 OrderItem。
实现: 嵌套结果映射 (Nested Result Map - 推荐)： 使用单条 SQL JOIN 查询（可能需要 LEFT JOIN 确保没有订单项的主订单也能查到）。
```xml
<resultMap id="orderWithItemsMap" type="Order">
    <id property="id" column="order_id"/>
    <result property="orderNumber" column="order_number"/>
    <!-- 其他 Order 属性映射 -->
    <collection property="orderItems" ofType="OrderItem">
        <id property="id" column="item_id"/> <!-- 集合元素需要自己的id -->
        <result property="productId" column="product_id"/>
        <result property="quantity" column="quantity"/>
        <result property="price" column="price"/>
        <!-- 其他 OrderItem 属性映射 -->
    </collection>
</resultMap>
<select id="selectOrderWithItems" resultMap="orderWithItemsMap">
    SELECT
        o.id AS order_id,
        o.order_number,
        oi.id AS item_id,
        oi.product_id,
        oi.quantity,
        oi.price
    FROM orders o
    LEFT JOIN order_items oi ON o.id = oi.order_id
    WHERE o.id = #{id}
</select>
```
## 自动映射
保持 PARTIAL，在 <resultMap> 中显式定义所有需要的映射（尤其关联和集合），利用 autoMapping="true" 仅在特定 <resultMap>, <association>, <collection> 上开启局部自动映射（当列名与属性名严格匹配且无需特殊处理时）。

```xml
<resultMap id="simpleOrderMap" type="Order" autoMapping="true">
    <id property="id" column="id"/> <!-- 即使autoMapping=true, id也建议显式写 -->
</resultMap>
<association property="customer" javaType="Customer" autoMapping="true"/> <!-- 嵌套对象自动映射 -->
```























# 动态SQL
动态SQL是指根据条件拼接SQL语句的功能，可以在SQL语句中添加或者删除某些条件和语句。在实际开发中，我们经常需要根据不同的条件拼接不同的SQL语句。如果只使用静态SQL，会使得代码冗余度高、可读性差、维护成本高等问题。而使用动态SQL可以很好地解决这些问题。
## if标签
它通常用来判断条件是否成立，从而确定是否加入SQL语句中。
```
<select id="findUser" resultType="User">
    SELECT * FROM user
    WHERE 1=1  <!-- 避免没有条件时SQL语法错误 -->
    <if test="name != null and name != ''">
        AND name = #{name}
    </if>
    <if test="age != null">
        AND age = #{age}
    </if>
</select>
```
上述代码中，通过if标签的test属性来判断条件是否成立。只有当"name"和"age"都不为空时，才会将其加入到SQL语句中。这样就可以在不同的情况下生成不同的SQL语句。
## where标签
自动添加 WHERE 关键字，并移除多余的 AND/OR
```
<select id="findUser" resultType="User">
    SELECT * FROM user
    <where>
        <if test="name != null">
            name = #{name}
        </if>
        <if test="age != null">
            AND age = #{age}
        </if>
    </where>
</select>
```
效果:
无参数时：SELECT * FROM user
只有 name 时：SELECT * FROM user WHERE name = ?
两个参数都有：SELECT * FROM user WHERE name = ? AND age = ?

## set标签 (智能处理 UPDATE 语句)
作用：自动添加 SET 关键字，并移除多余的逗号
```
<update id="updateUser">
    UPDATE user
    <set>
        <if test="name != null">name = #{name},</if>
        <if test="age != null">age = #{age},</if>
        <if test="email != null">email = #{email}</if>
    </set>
    WHERE id = #{id}
</update>
```

## choose、when和otherwise标签 (分支选择)
choose、when和otherwise标签通常一起使用，它类似于Java中的switch语句。
```
<select id="findUser" resultType="User">
    SELECT * FROM user
    <where>
        <choose>
            <when test="id != null">
                id = #{id}
            </when>
            <when test="name != null">
                name = #{name}
            </when>
            <otherwise>
                age > 18  <!-- 默认条件 -->
            </otherwise>
        </choose>
    </where>
</select>
```
条件按顺序匹配，一旦匹配成功则跳过后续条件
<otherwise> 是可选的

## trim标签 (自定义前缀和后缀处理)
等价替换：
<where> 等价于 <trim prefix="WHERE" prefixOverrides="AND |OR ">
<set> 等价于 <trim prefix="SET" suffixOverrides=",">

trim标签通常用来去掉特定字符或者关键字。
```
<select id="findUser" resultType="User">
    SELECT * FROM user
    <trim prefix="WHERE" prefixOverrides="AND |OR ">
        <if test="name != null">
            AND name = #{name}
        </if>
        <if test="age != null">
            OR age = #{age}
        </if>
    </trim>
</select>
```

## foreach标签 (循环处理集合参数)
作用：遍历集合（如 List、数组）生成重复 SQL 片段
场景：IN 条件、批量插入等
**示例 1**：查询 ID 在集合中的用户
```
<select id="findUsersByIds" resultType="User">
    SELECT * FROM user
    WHERE id IN
    <foreach item="id" collection="ids"
             open="(" separator="," close=")">
        #{id}
    </foreach>
</select>
```

**参数**：
-   `collection`：集合参数名（如 `ids`）
-   `item`：集合元素的临时变量名
-   `open/close`：生成 SQL 的起始 / 结束符号
-   `separator`：元素间的分隔符

**效果**：  
传入 `List<Integer> ids = [1,2,3]` →  
`SELECT * FROM user WHERE id IN (1,2,3)`

**示例 2**：批量插入数据

```
<insert id="batchInsert">
    INSERT INTO user (name, age)
    VALUES
    <foreach item="user" collection="list" separator=",">
        (#{user.name}, #{user.age})
    </foreach>
</insert>
```

### **7. `<bind>` 标签：自定义变量**

**作用**：在 SQL 中创建临时变量，常用于模糊查询  
**示例**：

```
<select id="findUserByName" resultType="User">
    <bind name="pattern" value="'%' + name + '%'" />
    SELECT * FROM user
    WHERE name LIKE #{pattern}
</select>
```