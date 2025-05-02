# 字符流
### 写入文件
``` java
public void Writetextfile(){
        String filename="hello.txt";
        try(BufferedWriter out=new BufferedWriter(new FileWriter(filename));)
        {
            out.write("hello");
            out.newLine();
        } catch (IOException e) {
            System.out.println("problem with"+filename);
        }
    }
```
### 读取文件
```java
public void Readtextfile()  {
        String filename="hello.txt";
        try(BufferedReader in=new BufferedReader(new FileReader(filename))) {
            String line=in.readLine();
            while(line!=null){
                System.out.println(line);
            }
        } catch (Exception e) {
            System.out.println("Problem with"+filename);
        }
    }

``` java
 public void Readtextfile()  {
        String filename="hello.txt";
        try(BufferedReader in=new BufferedReader(new FileReader(filename))) {
            int c=in.read();
            while(c!=-1){
                System.out.println((char)c);
                c=in.read();
            }
        } catch (Exception e) {
            System.out.println("Problem with"+filename);
        }
    }
````

# 字节流
### FileInputStream 是用于从文件中读取字节数据的类。
### BufferedInputStream 是 FileInputStream 的装饰器类，它提供了缓冲功能，可以提高文件读取的效率。
```java
 public void Readfile(){
        String filename="hello.txt";
        try(BufferedInputStream in=new BufferedInputStream(new FileInputStream(filename) )){
            int data=in.read();
            while(data!=-1){
                System.out.println(data);
                data=in.read();
            }
        } catch (Exception e) {
            System.out.println("Problem with"+filename);
        }
    }

```
---
### DataInputStream 是用于从输入字节流中读取基本数据类型的类，如整数、浮点数等。
``` java
public void ReadData(){
        String filename="data.bin";
        try(DataInputStream in=new DataInputStream(new FileInputStream(filename))){
            int num=in.readInt();
            double num1=in.readDouble();
            char ch=in.readChar();
        }catch(IOException e){
            e.printStackTrace();
        }
    }

```

---
### FileOutputStream 是用于将字节数据写入文件的类。
### BufferedOutputStream 是 FileOutputStream 的装饰器类，它提供了缓冲功能，可以提高文件写入的效率。
``` java
public void WriteFile(){
        String filename="hello.txt";
        try(BufferedOutputStream out=new BufferedOutputStream(new FileOutputStream(filename))){
            String txt="hello !";
            byte[] bytes=txt.getBytes();
            out.write(bytes);
        }catch (IOException e){
            e.printStackTrace();
        }
    }

```
### DataOutputStream 是用于将基本数据类型写入输出字节流的类，与 DataInputStream 相对应。
```java
public void WriteData(){
        String filename="data.bin";
        try(DataOutputStream out=new DataOutputStream(new FileOutputStream(filename))){
            int num=12;
            double num1=12.1;
            char ch='a';
            out.writeInt(num);
            out.writeDouble(num1);
            out.writeChar(ch);
        }catch (IOException e){
            e.printStackTrace();
        }
    }

```
---
# 复制文件
```java
public void CopyFile(){
        String filea="a.bin";
        String fileb="b,bin";
        try(BufferedInputStream in=new BufferedInputStream(new FileInputStream(filea));
            BufferedOutputStream out=new BufferedOutputStream(new FileOutputStream(fileb))
        ){
            byte[] buffer=new byte[1024];
            int bytesRead;
            while((bytesRead=in.read(buffer))!=-1){
                out.write(buffer,0,bytesRead);
            }
        }catch (IOException e){
            e.printStackTrace();
        }
    }
```

# Java提供了对象的序列化和反序列化功能，可以将对象转换为字节流以进行存储或传输，然后再将其还原为对象。
不会保存和读取transient和static修饰的成员变量  
序列化的对象要实现Serializable接口


``` java
class Person implements Serializable{
    String name;
    int age;
    transient String id;
    public  Person(){}
    public Person(String name,int age,String id ){
        this.name=name;
        this.age=age;
        this.id=id;
    }
    static public void Serialization(String filename,Person p){
        try(ObjectOutputStream out=new ObjectOutputStream(new FileOutputStream(filename))){
            out.writeObject(p);
        }catch(IOException e){
           System.out.println("Serialization error");
           e.printStackTrace();
        }
    }
    static public Person Deserialization(String filename){
        try(ObjectInputStream in=new ObjectInputStream(new FileInputStream(filename))){
            Person pe=(Person)in.readObject();
            return pe;
        }catch(Exception e){
           System.out.println("Deserialization error");
           e.printStackTrace();
        }
        return null;
    }
}
```
