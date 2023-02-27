# Prime Numbers

```java
public class Main {

    public static void main(String[] args) {


        for (int num = 2; num < 1000; num++) {
            boolean isPrime = true;

            for (int div = 2; div * div <= num; div++) {

                if(num % div == 0) {
                    isPrime = false;
                    break;
                }
            }

            if (isPrime) {
                System.out.println(num);
            }
        }

    }
}
```