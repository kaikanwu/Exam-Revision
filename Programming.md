
## Java Basic
* Object Oriented Programming

* 关键字
    - private
    - static
    - final

* [statement](https://github.com/kaikanwu/Exam-Revision/blob/master/Programming.md#Statement)
    - if
    - while 
    - [for](https://github.com/kaikanwu/Exam-Revision/blob/master/Programming.md##for)
    - [switch](https://github.com/kaikanwu/Exam-Revision/blob/master/Programming.md##switch)






# Statement

## for 
```
for(initializaiton;termination; increment){
    statement(s)
}
```
* examples:
```
for(int i = 0; i < 100; i++){
    ...
    System.out.println("Count is: " + i );

}
```
```
// infinate loop

for(;;){
    //code
}
```




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

## switch
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


