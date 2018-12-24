<small>
###IO流
I:input，O:output,又称为输入输出流。
输入：读取操作，输出：写出操作（要站在内存的立场上理解）
根据功能不同分为：输出流，输入流，字节流，字符流，低级流，节点流，处理流，这里我们将学习 字节输入输出流和字符输入输出流
######FileOutputStream
字节输出流，可以直接地文件，惊醒写出操作，可以单字节的写，也可以批量字节的写
有两个构造方法和RandomAccessFile相似，抽象地址所在的路径必须操作，否则抛出异常，如果抽象地址所在路径存在，但文件不存在，会自动创建文件
**最大特点是可以实现追加写出操作**
如果想要创建可以实现追加写出操作的字节输出流，那必须使用下面的构造：
new FileOutputStream(String pathName,boolean isAppend)
isAppeend为是否追加

#####FileInputStream
抽象地址必须存在，否则抛出异常
> 一个中文字符，GBK为两个字节，UTF-8为三个字节，一个英文字符，无论GBK还是UTF-8都是一个字节

#####BufferedOutputStream
缓冲字节输出流
不能直接对接文件或者虚拟地址，必须和一个输出流对接
new BufferedOutputStream(new(FileOutputStream) )
#####BufferedInputStream
缓冲字节输入流（读写文件），特点：自身维护一个字节数组，提携文件的读写效率，BufferedOutputStream也是如此。
```
	public static void main(String[] args) throws IOException {
		/*
		 * FileInputStream构造方法
		 * 		new FileInputStream(String pathName)
		 * 
		 * 		new FileInputStream(File file)
		 * 			
		 * 		注意：1、抽象地址文件必须存在，否则抛出异常。
		 * 
		 */
		FileInputStream fis = 
					new FileInputStream(new File("fos.txt"));
		/*
		 * 1、单字节的读取
		 * 		int read();
		 */
		int read = fis.read();
		System.out.println(read);//98
		fis.read();//100
		fis.read();//128
		
		/*
		 * 2、批量字节读取
		 * 		int read(byte[] buf)
		 * 		返回真正读取的字节数。
		 */
		byte[] buf = new byte[100];
		int read2 = fis.read(buf);
		//将字节数组，转换成字符串
		String str = new String(buf,0,read2,"UTF-8");
		System.out.println(str);
		
		fis.close();
	}

}
```
```
public static void main(String[] args) throws IOException {
		/*
		 * FileOutputStream构造方法
		 * 		new FileOutputStream(String pathName)
		 * 
		 * 		new FileOutputStream(File file)
		 * 			
		 * 		注意：1、抽象地址所在路径必须存在，否则抛出异常。
		 * 			 2、抽象地址所在路径存在，但文件不存在，
		 * 				则会自动创建文件。
		 * 
		 */
		FileOutputStream fos = 
					new FileOutputStream(new File("fos.txt"));
		/*
		 * 1、写出一个字节
		 * 		write(int i)
		 */
		fos.write(98);
		
		fos.close();
		
		/*
		 * 如果想创建可以实现追加写出操作的字节输出流
		 * 		那必须使用下面构造：
		 * 		new FileOutputStream(String pathName, boolean isAppend)
		 * 
		 * 		new FileOutputStream(File file, boolean isAppend)
		 * 
		 * 		isAppend为是否追加写出标识，默认是false。
		 * 		true标识追加写出。
		 */
		fos = new FileOutputStream("fos.txt",true);
		fos.write(100);
		fos.write(128);
		
		/*
		 * 2、批量字节写出
		 * 		write(byte[] buf)
		 */
		String str = "我爸叫李刚";
		byte[] buf = str.getBytes("UTF-8");
		fos.write(buf);
		
		fos.close();
```

#####ObjectOutputStream
new ObjectOutputStream()
如果想让people对象，完成持久化（传输保存）到硬盘中，则people必须为可序列化.
序列化：将需要持久化的数据，转换成字节类型数据。
对象序列化：将需要持久化的引用类型对象，转换成字节类型数据。
序列化接口，仅为标识接口，没有任何抽象方法。
只要类实现该接口，就意味着可以进行持久化操作。
```
public static void main(String[] args) throws FileNotFoundException, IOException, ClassNotFoundException {
  // TODO Auto-generated method stub
  ObjectOutputStream oos=new ObjectOutputStream(
    new BufferedOutputStream(
      new FileOutputStream("/Users/itachi/Downloads/demo1.txt")));
  People peo=new People("Jack",18,'M');
  oos.writeObject(peo);
  oos.close();
  ObjectInputStream ois=new ObjectInputStream(
    new BufferedInputStream(
      new FileInputStream("/Users/itachi/Downloads/demo1.txt")));
  Object obj=ois.readObject();
  System.out.println(obj);
 }

}
class People implements Serializable {
                 默认添加序列化的版本号
	 * 		用于在写出读取对象信息时，
	 * 		验证对象是否为同一个对象。
 private static final long serialVersionUID = 1L;
 private String name;
 private int age;
 private char gendar;
/*
	 * 如果对于不需要保存的字段，
	 * 	可以通过transient关键字，
	 * 	直接作用在字段上，就不会被保存。
	 * 	从而一定程度对象实现“瘦身”效果。
	 */
	transient
	private double salary;
  
 public People() {
 }
 
 public People(String name, int age, char gendar) {
  this.name = name;
  this.age = age;
  this.gendar = gendar;
 }

 public String getName() {
  return name;
 }
 public void setName(String name) {
  this.name = name;
 }
 public int getAge() {
  return age;
 }
 public void setAge(int age) {
  this.age = age;
 }
 public char getGendar() {
  return gendar;
 }
 public void setGendar(char gendar) {
  this.gendar = gendar;
 }

 @Override
 public String toString() {
  return " [getName()=" + getName() + ", getAge()=" + getAge()
    + ", getGendar()=" + getGendar() + "]";
```

