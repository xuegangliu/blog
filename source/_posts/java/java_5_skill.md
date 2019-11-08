title: JDK1.5新特性
comments: true
date: 2019-11-06 10:30:12
updated: 2019-11-06 10:30:12
tags:
  - java_base
  - knowledge
categories:
  - java
---

### JDK1.5新特性

1. 自动装箱与拆箱
    基本数据类型与封装的基本类型互相转换

2. 枚举
    java.lang.Enum
``` java
package java.lang.annotation;

/**
 * Annotation retention policy.  The constants of this enumerated type
 * describe the various policies for retaining annotations.  They are used
 * in conjunction with the {@link Retention} meta-annotation type to specify
 * how long annotations are to be retained.
 *
 * @author  Joshua Bloch
 * @since 1.5
 */
public enum RetentionPolicy {
    /**
     * Annotations are to be discarded by the compiler.
     */
    SOURCE,

    /**
     * Annotations are to be recorded in the class file by the compiler
     * but need not be retained by the VM at run time.  This is the default
     * behavior.
     */
    CLASS,

    /**
     * Annotations are to be recorded in the class file by the compiler and
     * retained by the VM at run time, so they may be read reflectively.
     *
     * @see java.lang.reflect.AnnotatedElement
     */
    RUNTIME
}
```

3. 静态导入
`import static java.lang.Math.PI;`

4. 可变参数（Varargs）
```java
/**
 * A
 * <p>
 * This is description
 * </p>
 *
 * @author xuegangliu 2019/11/06
 * @since 1.8
 **/
public class A {

    public static void main(String[] args) {
        new A().test(1,2,3,4,5);
    }
    public void test(int... a){
        for(int t:a){
            System.out.println(t);
        }
    }
}
```

5. 内省（Introspector），访问某个对象属性的 getter/setter 方法的API。
`java.beans.*`

6. 泛型(Generic)（包括通配类型/边界类型等）

7. For-Each循环

8. 注解

9. 协变返回类型：实际返回类型可以是要求的返回类型的一个子类型


<details>
  <summary>5.6.7.8.9代码示例</summary>
  <br/>
  <code>
package org.lxg.basic.jdk5;

import lombok.extern.slf4j.Slf4j;
import org.junit.Test;
import org.lxg.basic.annotation.AnnotationA;
import org.lxg.basic.annotation.AnnotationB;
import org.lxg.basic.annotation.BasicInfo;
import org.lxg.basic.annotation.filed.BaseFiled;
import org.lxg.basic.annotation.method.BasicMethod;

import java.beans.BeanInfo;
import java.beans.IntrospectionException;
import java.beans.Introspector;
import java.beans.PropertyDescriptor;
import java.lang.reflect.Field;
import java.lang.reflect.InvocationTargetException;
import java.lang.reflect.Method;
import java.util.ArrayList;
import java.util.List;

import static java.lang.Math.max;

/**
 * Jdk5Tests
 * <p>
 * This is description
 * </p>
 *
 * @author xuegangliu 2019/11/06
 * @since 1.8
 **/
@Slf4j
public class Jdk5Tests {
    @Test
    public void testAnnotationA(){
        Class clsA = AnnotationA.class;
        log.info("clsA class:{}",clsA.getName());

        BasicInfo basicTypeA = (BasicInfo) clsA.getAnnotation(BasicInfo.class);
        log.info("clsA {},{}",basicTypeA.version(),basicTypeA.description());


        Field[] fields1 = clsA.getDeclaredFields();
        log.info("----------- field -------------------");
//        Field[] fields = clsA.getFields();
//        for (Field field : fields) {
//            BaseFiled baseFiled = field.getAnnotation(BaseFiled.class);
//            if (baseFiled != null) {
//                log.info("field:{},{},{}",field.getName(),baseFiled.description(),baseFiled.Old());
//            }
//        }
        for (Field field : fields1) {
            BaseFiled baseFiled = field.getAnnotation(BaseFiled.class);
            if (baseFiled != null) {
                log.info("field:{},{},{}",field.getName(),baseFiled.description(),baseFiled.Old());
            }
        }
        log.info("------------ methods ------------------");
        Method[] methods = clsA.getDeclaredMethods();
        for(Method method:methods){
            BasicMethod methodInfo=method.getAnnotation(BasicMethod.class);
            if(methodInfo!=null){
                log.info("Annotation: method:{},author:{},date:{},version:{}",method.getName(),methodInfo.author(),methodInfo.date(),methodInfo.version());
            }
        }
    }

    @Test
    public void testAnnotationB(){
        Class clsB = AnnotationB.class;
        log.info("clsB class:{}",clsB.getName());

        BasicInfo basicTypeB = (BasicInfo) clsB.getAnnotation(BasicInfo.class);
        log.info("clsB {},{}",basicTypeB.version(),basicTypeB.description());


        Field[] fields1 = clsB.getDeclaredFields();
        log.info("----------- field -------------------");
//        Field[] fields = clsA.getFields();
//        for (Field field : fields) {
//            BaseFiled baseFiled = field.getAnnotation(BaseFiled.class);
//            if (baseFiled != null) {
//                log.info("field:{},{},{}",field.getName(),baseFiled.description(),baseFiled.Old());
//            }
//        }
        for (Field field : fields1) {
            BaseFiled baseFiled = field.getAnnotation(BaseFiled.class);
            if (baseFiled != null) {
                log.info("field:{},{},{}",field.getName(),baseFiled.description(),baseFiled.Old());
            }
        }
        log.info("------------ methods ------------------");
        Method[] methods = clsB.getDeclaredMethods();
        for(Method method:methods){
            BasicMethod methodInfo=method.getAnnotation(BasicMethod.class);
            if(methodInfo!=null){
                log.info("Annotation: method:{},author:{},date:{},version:{}",method.getName(),methodInfo.author(),methodInfo.date(),methodInfo.version());
            }
        }
    }

    @Test
    public void testBox(){
        int i=1;
        Integer j=i;
        log.error("int i:{},Integer j:{}",i,j);

        Integer x=256;
        int y=x;
        log.error("Integer x:{},int y:{}",x,y);
    }

    @Test
    public void testEnum(){
        for (EnumA e : EnumA.values()) {
            log.error("code:{},msg:{}",e.code,e.msg);
        }
    }

    @Test
    public void testImportStatic(){
        log.error("(import static java.lang.Math.max) max(11,12):{}",max(11,12));
    }

    @Test
    public void testChangeArgs(){
        Jdk5Tests.changeArgs(1,2,3,5,4);
    }

    @Test
    public void testBeanGetSet() throws IntrospectionException, InvocationTargetException, IllegalAccessException {
        Student student = new Student("Tony",28);

        PropertyDescriptor propertyDescriptorName = new PropertyDescriptor("name", Student.class);
        Method writeNameMethod = propertyDescriptorName.getWriteMethod();
        Method readNameMethod = propertyDescriptorName.getReadMethod();
        log.error("{}",readNameMethod.invoke(student).toString());
        writeNameMethod.invoke(student, "Tony1");
        log.error("{}",readNameMethod.invoke(student).toString());

        BeanInfo beanInfo = Introspector.getBeanInfo(student.getClass());
        PropertyDescriptor[] pd = beanInfo.getPropertyDescriptors();
        for (int i = 0; i < pd.length; i++) {
            PropertyDescriptor p=pd[i];
            log.error("{}",p.getName());
        }
    }

    @Test
    public void testGeneric(){
        List<Integer> list = new ArrayList<Integer>();
        list.add(1);
//        list.add("err");
        log.error("size:{}",list.size());
    }

    @Test
    public void testForEach(){
        Student tony=new Student("Tony",11);
        Student lily=new Student("Lily",13);
        List<Student> list=new ArrayList<Student>();
        list.add(tony);
        list.add(lily);

        for (Student student : list) {
            log.error("name:{},age:{}",student.getName(),student.getAge());
        }
    }

//    public ? super Student changeReturn(){
//
//        return null;
//    }

    public static void changeArgs(int... args){
        for (int i = 0; i < args.length; i++) {
            log.error("{}",args[i]);
        }
    }

    private enum EnumA{
        OK(200,"OK"),
        NO(404,"No");

        private String msg;
        private Integer code;
        EnumA(Integer code,String msg){
            this.msg=msg;
            this.code=code;
        }
    }
}
class Base{

    public Base(){}

    public List<Object> getList(){
        return new ArrayList<>();
    }

}

class Student extends Base{
    private String name;
    private Integer age;

    public Student(String name,Integer age){
        this.name=name;
        this.age=age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Integer getAge() {
        return age;
    }

    public void setAge(Integer age) {
        this.age = age;
    }

    @Override
    public ArrayList<Object> getList(){
        // 重新父类方法,返回值是父类返回值的子类即协变返回类型
        return new ArrayList<>();
    }
}

  </code>
</details>