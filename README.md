###  [Task 7 kyu](https://www.codewars.com/kata/634d0f7c562caa0016debac5/train/java)
Given two Arrays in which values are the power of each soldier, return true if you survive the attack or false if you perish.

CONDITIONS

    Each soldier attacks the opposing soldier in the same index of the array. The survivor is the number with the highest value.
        If the value is the same they both perish
        If one of the values is empty(different array lengths) the non-empty value soldier survives.
    To survive the defending side must have more survivors than the attacking side.
    In case there are the same number of survivors in both sides, the winner is the team with the highest initial attack power. If the total attack power of both sides is the same return true.
        The initial attack power is the sum of all the values in each array.


### My solution
```Java
import java.util.Arrays;

public class Kumite{
    public static boolean block(int[] attackers, int[] defenders){
        int survivorsCount = 0;

        int lengthDiff = attackers.length - defenders.length;

        for ( int i = 0; i < Math.min(attackers.length, defenders.length); i++) {
            if (attackers[i] - defenders[i] < 0) {
                survivorsCount += 1;
            } else if (attackers[i] - defenders[i] > 0){
                survivorsCount -= 1;
            }
        }

        if (lengthDiff < 0) {
            survivorsCount += Math.abs(lengthDiff);
        } else {
            survivorsCount -= lengthDiff;
        }

        int damage = Arrays.stream(attackers).sum() - Arrays.stream(defenders).sum();

        if (survivorsCount < 0) {
            return false;
        } else if (survivorsCount > 0) {
            return true;
        } else if (damage > 0){
            return false;
        }

        return true;
    }
}



```

### Fav solution
```Java
import java.util.Arrays;

public class Kumite{
    public static boolean block(int[] attackers, int[] defenders) {
        int res = defenders.length - attackers.length;
        for (int i = 0; i < Math.min(attackers.length, defenders.length); i++) {
            res += attackers[i] < defenders[i] ? 1 : attackers[i] > defenders[i] ? -1 : 0;
        }
        return res > 0 || (res == 0 && Arrays.stream(defenders).sum() >= Arrays.stream(attackers).sum());
    }
}
```
I like this solution because I like it
