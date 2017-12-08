---
title: 原生Java使用druid数据库连接池
date: 2017-12-08 11:09:57
categories: Java
tags: 
 - Java
 - druid
---
不依赖spring，直接使用druid数据库连接池，这样写原生java对数据库的操作也不需要自己去分配与管理数据库连接，重复使用现有连接，不需要每次都新建连接，这可以大大提升数据库的处理效率
# ConnectionFactory数据库连接的工厂类
其中包含了druid数据库连接池的配置，还有从数据库连接池中获取数据库连接的操作
{% codeblock %}
import com.alibaba.druid.pool.DruidDataSource;

import java.sql.Connection;
import java.sql.SQLException;

/**
 * @Author:langxy
 * @date 创建时间：2017/12/2 10:54
 */
public class ConnectionFactory {
    private static DruidDataSource druidDataSource = null;

    static {
        try {
            String driver = "com.mysql.jdbc.Driver";
            String url = "jdbc:mysql://127.0.0.1:3306/computer?characterEncoding=utf-8";
            String username = "root";
            String password = "";

            druidDataSource = new DruidDataSource();
            druidDataSource.setDriverClassName(driver);
            druidDataSource.setUrl(url);
            druidDataSource.setUsername(username);
            druidDataSource.setPassword(password);
            druidDataSource.setInitialSize(5);
            druidDataSource.setMinIdle(1);
            druidDataSource.setMaxActive(10);

            druidDataSource.setPoolPreparedStatements(false);
        } catch (Exception e){
            e.printStackTrace();
        }
    }
    public static synchronized Connection getConnection(){
        Connection conn = null;
        try {
            conn = druidDataSource.getConnection();
        } catch (SQLException e) {
            e.printStackTrace();
        }
        return conn;
    }
}
{% endcodeblock %}

# DbAction类数据库操作的类
这里我们只写了一个查找操作的方法为例子，数据库操作完成后，把连接交给druid，接着由druid去分配与管理
{% codeblock %}
import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;

/**
 * @Author:langxy
 * @date 创建时间：2017/12/8 8:55
 */
public class DbAction {

    public static Connection conn = null;
    public static PreparedStatement pstmt = null;
    public static ResultSet rs = null;
    
    public static void main(String[] args) {
        conn = ConnectionFactory.getConnection();
        String sql = "select * from information";
        try {
            pstmt = conn.prepareStatement(sql);
            rs = pstmt.executeQuery();
            while (rs.next()){
                System.out.println(rs.getString("username"));
                System.out.println(rs.getString("password"));
            }
            System.out.println("Success");
        } catch (SQLException e) {
            System.out.println(String.format("失败, %s", e.getMessage()));
        } finally {
            if (rs != null){
                try {
                    rs.close();
                } catch (Exception e){
                    e.printStackTrace();
                }
            }
            if (pstmt != null){
                try {
                    pstmt.close();
                } catch (Exception e){
                    e.printStackTrace();
                }
            }
            if (conn != null){
                try {
                    conn.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
{% endcodeblock %}
