Given an array `nums` of size `n`, return *the majority element*.

The majority element is the element that appears more than `⌊n / 2⌋` times. You may assume that the majority element always exists in the array.

> The question is asking for taking the most common element in an array

### M1: HashMap

```java
public int majorityElement(int[] nums){
   Map<Integer,Integer> map = new HashMap<Integer,Integer>();
   int res = 0;
   for(int num: nums){
      if(!map.containsKey(num)){
         map.put(num,1);
      } else{
         map.put(num,map.get(num)+1);
      }
      if(map.get(num) > nums.length/2){
         res = num;
         break;
      }
   }
   return res;
}
```

The idea is to use the hashmap and check the common element. In general, this type of question should run O(n);

### M2: Voting algorithm

```java
public int majorityElement(int[] nums){
      int count=0, major = 0;
      for (int num: nums) {
         if (count==0) major = num;

         if (num!=major) count--;
         else count++;
      }
   return major;
}
```

when using this algothorim, you have to know the question is asking for the majority element that is accounting for at least half of the array, otherwise don't consider it in this way. I wouldn't go very detail about this, because there are tons of reserach paper and Mathmathical proof behind this.

The idea behind this algorithm is to delete two different element in an array and what's remained is the majority.

```
Let's say we have an array. int[] arr = {1,2,3,4,1,1,1}; and another virtual array{}

count = 0; the number is 1; put into v-array{1}

count = 1; the number is 2; put into v-array{1,2}, delete both element ⇒ {}

count = 2; the number is 3; put into v-array{3}

count = 3; the number is 4; put into v-array{3,4}; delete it⇒{}

count = 4; the number is 1; put into v-array{1}

count = 5; the number is 1; put into v-array{1,1}

count = 6; the number is 1; put into v-array{1,1,1}

count = 7; the number is 1; put into v-array{1,1,1,1}

In the end, the result is 1
```
