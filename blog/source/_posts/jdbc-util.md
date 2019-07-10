---
title: jdbc获取连接工具
date: 2016-05-29 21:28:34
tags:
- java
categories: java
---
所需属性文件：jdbc.properties

    ## ORACLE
    #jdbc.driver=oracle.jdbc.OracleDriver
    	#jdbc.url=jdbc:oracle:thin:@localhost:1521:yfs_database
    #jdbc.username=scott
    #jdbc.password=tiger
    
    
    ## SQL SERVER
    	#jdbc.driver=com.microsoft.jdbc.sqlserver.SQLServerDriver
    #jdbc.url=jdbc:microsoft:sqlserver://localhost:1433;databaseName=yfs_database
    #jdbc.username=sa
    #jdbc.password=
    
    
    ## Access
    #jdbc.driver=sun.jdbc.odbc.JdbcOdbcDriver
    #jdbc.url=jdbc:odbc:driver={Microsoft Access Driver (*.mdb)};DBQ=user.mdb
    #jdbc.username=
    #jdbc.password=
    
    ## My SQL
    jdbc.driver=com.mysql.jdbc.Driver
    jdbc.url=jdbc:mysql://localhost:3306/yfs_database
    jdbc.username=root
    jdbc.password=root

获取连接类：JdbcUtil.java

    package com.yfs.jdbc;
    
    import java.io.IOException;
    import java.io.InputStream;
    import java.sql.Connection;
    import java.sql.DriverManager;
    import java.sql.ResultSet;
    import java.sql.SQLException;
    import java.sql.Statement;
    import java.util.Properties;
    
    public class JdbcUtil {
    	  private static String driver;
    	  private static String url;
    	  private static String username;
    	  private static String password;
    	  static {
    		 Properties prop = new Properties();//读取配置文件
    		 InputStream  in = JdbcUtil.class.getResourceAsStream("jdbc.properties");
    		 try {
    			prop.load(in);//加载文件
    			driver = prop.getProperty("jdbc.driver");
				// 数据库信息
    			url = prop.getProperty("jdbc.url");
    			username = prop.getProperty("jdbc.username");
    			password = prop.getProperty("jdbc.password");
    			System.out.println(driver);
    			System.out.println(url);
    			System.out.println(username);
    			System.out.println(password);
    			Class.forName(driver);// 加载数据库驱动
    		} catch (IOException e) {
    			e.printStackTrace();
    		} catch (ClassNotFoundException e) {
    			e.printStackTrace();
    		}
    		 
    	  }
    	  
    	  //获取链接
    	  public static Connection getConnection () {
    		  Connection conn = null;
    		  try {
    			conn = DriverManager.getConnection(url,username,password);
    		} catch (SQLException e) {
    			//e.printStackTrace();
    			System.out.println("数据库链接失败");
    		}
    		  return conn;
    	  }
    	  
    	  public static void release(ResultSet rs, Statement st, Connection conn){
    		  try {
				//关闭结果集
    			if(rs != null){
    				  rs.close();
    			  }
    		} catch (SQLException e) {
    			e.printStackTrace();
    		} finally {
    			try {
					// 关闭执行对象
    				if(st != null){
    					st.close();
    				}
    			} catch (SQLException e) {
    				e.printStackTrace();
    			} finally {
    				try {
						// 关闭链接
    					if(conn != null) {
    						conn.close();
    					}
    				} catch (SQLException e) {
    					e.printStackTrace();
    				}
    			}
    		}
    	  }
    }

测试创建表、插入数据、更新数据类：JdbcDemo.java

    package com.yfs.jdbc;
    
    import java.sql.Connection;
    import java.sql.DriverManager;
    import java.sql.SQLException;
    import java.sql.Statement;
    
    public class JdbcDemo1 {
    
    	public static void main(String[] args) throws Exception {
    		executeEmp();
    	}
    
    	public static void executeEmp() {
    		Connection conn = JdbcUtil.getConnection();
    		Statement st = null;
    		try {
				// 执行对象
    			st = conn.createStatement();
				//创建表
				//String sql = "create table emp(emp_id int primary key, ename varchar(30) not null, sex char(2),job varchar(20), sal int)";
				//插入
				//String sql = "insert into emp values(1,'张三','男','经理',8000)";
				//更新
    			String sql = "update emp set sal=sal+2000 where emp_id=1";
    			st.execute(sql);
    		} catch (SQLException e) {
    			e.printStackTrace();
    		} finally {
    			JdbcUtil.release(null, st, conn);
    		}
    		System.out.println("更新成功");
    	}
    }

