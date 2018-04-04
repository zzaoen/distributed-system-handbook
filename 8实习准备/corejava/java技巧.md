
# 格式化输出
```
out.printf("%,+.2f\n", 10000.0/3.0);
String message = String.format("The averag number is: %,+.2f, total number: %d ", 10000.0/3, 10000);
out.println(message);
%d、%x、%o分别是10、16和8进制，没有2进制。
```
# 数组的复制
```
int[] array = new int[]{1,2,3};
int[] arrayCopy = array;
arrayCopy[2] = 30;
for(int i : array)
    out.print(i);
int[] arrayDeepCopy = Arrays.copyOf(array, array.length);
arrayDeepCopy[2] = 300;
for(int i : array)
out.print(i);
```


# Cool

```
Map<String, Integer> map = new HashMap<>();
map.put("alice", 1);
map.put("alice", 2);
map.merge("alice", 1, Integer::sum); //{alice=3}
//或者也可以
map.merge("alice", 1, (x, y)->Integer.sum(x, y)); //{alice=4}
out.println(map);
```
```
merge("alice", 1, Integer::sum)
```
如果map中存在"alice"，会把之前的值加1，如果不存在，赋值为1。



# 排序

## Comparable

一个对象数组，排序算法需要重复比较数组中的元素。不同的类比较元素的规则是不同的，但是排序算法只应该调用类提供的比较方法，只要所有的类就比较的时候提供的方法达成一致，那么排序算法就能开始工作。这个在排序时对象之间进行比较方法就可以是一个接口，所有需要比较的对象继承这个接口并且实现比较的方法，就可以对这些对象进行排序。

如果一个类想启用对象排序，那么就应该实现Comparable接口。

```java
public class Test{
	public static void main(String[] args){
        Employee[] employees = new Employee[3];
        employees[0] = new Employee(20);
        employees[1] = new Employee(10);
        employees[2] = new Employee(30);
        Arrays.sort(employees);
        for(Employee e : employees){
        	System.out.println(e);
        }
	}
	
	static class Employee implements Comparable<Employee>{ //因为在main方法中实例化这个类，所以只能是static的
        private int id;
        public Employee(int id){this.id = id;}
        @Override
        public int compareTo(Employee o) {
            return this.id - o.id;
        }
        @Override
        public String toString() {
            return "Employee{" + "id=" + id + '}';
        }
	}
}

```





## Comparator

假如想根据字符串的长度而不是根据字典顺序对字符串排序，但是String类我们是无法修改的。

Arrays.sort方法和Collections.sort方法都提供了一个可以接收Comparator实例作为第二个参数的版本。

要按照长度比较字符串，定义一个实现Comparator<String>的类。

```java
public class LengthComparator implements Comparator<String> {
    @Override
    public int compare(String o1, String o2) {
    	return o1.length() - o2.length();
    }
    public static void main(String[] args){
        String[] names = {"tom", "alice", "fred"};
        Arrays.sort(names, new LengthComparator());
        out.println(Arrays.toString(names));
    }
}

```

