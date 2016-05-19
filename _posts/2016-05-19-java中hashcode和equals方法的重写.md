---
layout: post
title: java中hashcode和equals方法的重写
date: 2016-5-19
categories: blog
tags: [java, 总结]
---

使用hashCode()和equals()

hashCode()方法被用来获取给定对象的唯一整数。这个整数被用来确定对象被存储在HashTable类似的结构中的位置。默认的，Object类的hashCode()方法返回这个对象存储的内存地址的编号。

重写默认的实现

如果你不重写这两个方法，将几乎不遇到任何问题，但是有的时候程序要求我们必须改变一些对象的默认实现。

来看看这个例子，让我们创建一个简单的类Employee

	public class Employee
	{
	    private Integer id;
	    private String firstname;
	    private String lastName;
	    private String department;
	 
	    public Integer getId() {
	        return id;
	    }
	    public void setId(Integer id) {
	        this.id = id;
	    }
	    public String getFirstname() {
	        return firstname;
	    }
	    public void setFirstname(String firstname) {
	        this.firstname = firstname;
	    }
	    public String getLastName() {
	        return lastName;
	    }
	    public void setLastName(String lastName) {
	        this.lastName = lastName;
	    }
	    public String getDepartment() {
	        return department;
	    }
	    public void setDepartment(String department) {
	        this.department = department;
	    }
	}
	
上面的Employee类只是有一些非常基础的属性和getter、setter.现在来考虑一个你需要比较两个employee的情形。

	public class EqualsTest {
	    public static void main(String[] args) {
	        Employee e1 = new Employee();
	        Employee e2 = new Employee();
	 
	        e1.setId(100);
	        e2.setId(100);
	        //Prints false in console
	        System.out.println(e1.equals(e2));
	    }
	}
	
毫无疑问，上面的程序将输出false，但是，事实上上面两个对象代表的是通过一个employee。真正的商业逻辑希望我们返回true。 
为了达到这个目的，我们需要重写equals方法。 

	public boolean equals(Object o) {
	        if(o == null)
	        {
	            return false;
	        }
	        if (o == this)
	        {
	           return true;
	        }
	        if (getClass() != o.getClass())
	        {
	            return false;
	        }
	        Employee e = (Employee) o;
	        return (this.getId() == e.getId());
	}
在上面的类中添加这个方法，EauqlsTest将会输出true。 
让我们换一种测试方法来看看。 
?
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
import java.util.HashSet;
import java.util.Set;
 
	public class EqualsTest
	{
	    public static void main(String[] args)
	    {
	        Employee e1 = new Employee();
	        Employee e2 = new Employee();
	 
	        e1.setId(100);
	        e2.setId(100);
	 
	        //Prints 'true'
	        System.out.println(e1.equals(e2));
	 
	        Set<Employee> employees = new HashSet<Employee>();
	        employees.add(e1);
	        employees.add(e2);
	        //Prints two objects
	        System.out.println(employees);
	    }
上面的程序输出的结果是两个。如果两个employee对象equals返回true，Set中应该只存储一个对象才对，问题在哪里呢？ 
我们忘掉了第二个重要的方法hashCode()。就像JDK的Javadoc中所说的一样，如果重写equals()方法必须要重写hashCode()方法。我们加上下面这个方法，程序将执行正确。

	@Override
	 public int hashCode()
	 {
	    final int PRIME = 31;
	    int result = 1;
	    result = PRIME * result + getId();
	    return result;
	 }

