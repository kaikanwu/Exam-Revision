
## Java Basic
* Object Oriented Programming

* 关键字
    - private
    - static
    - final

* [statement](https://github.com/kaikanwu/Exam-Revision/blob/master/Programming.md#statement)
    - if
    - while 
    - [for](https://github.com/kaikanwu/Exam-Revision/blob/master/Programming.md#for-语句)
    - [switch](https://github.com/kaikanwu/Exam-Revision/blob/master/Programming.md#switch-语句)






# Statement

## for 语句 
```
for(initializaiton;termination; increment){
    statement(s)
}
```
* examples:
1. 基础
```
for(int i = 0; i < 100; i++){
    ...
    System.out.println("Count is: " + i );
}
```
2. infinate loop 无限循环
```


for(;;){
    //code
}
```
3. 遍历数组
```
// used for array

int[] numbers = {1,2,3,4,5,6,7,8,9};

for(int x : numbers){
    System.out.println(x);
}
//output of this program:
// 1
// 2
// 3
// ...
```

## switch 语句
```


public class SwitchDemo {
    public static void main(String[] args) {

        int month = 8;
        String monthString;
        switch (month) {
            case 1:  monthString = "January";
                     break;
            case 2:  monthString = "February";
                     break;
            case 3:  monthString = "March";
                     break;
            ...

            case 8:  monthString = "August";
                     break;
            ...
         
            default: monthString = "Invalid month";
                     break;
        }
        System.out.println(monthString);
    }
}
```


