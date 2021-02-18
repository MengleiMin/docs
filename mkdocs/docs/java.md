## Optional  
-  `getData(input).isPresent()`   
-  `getData(input).isEmpty()` 

- 
    /* Return non-negative value, and when result is null, return 0L */

        private long getA(Optional<QueryResponse> response) {
                return response
                        .map(r -> r.b)
                        .map(b -> Math.max(0, b)
                        .orElse(0L);
        }
  
- 
    /* Return non-negative value, when result is null, return result/null */

        private long getA(Optional<QueryResponse> response) {
                return response
                        .map(r -> r.b)
                        .map(b -> Math.max(0, b)
                        .get();
        }

- 
     /* Return the result which A.getB() >= b and sort it out as ascending order by C */

        private long getC(Object A) {
            return A.stream()
                    .filter(A -> A.getB() >= b)
                    .max(Comparator.comparing(A::getC()))
                    .map(A::getC())
                    .orElse(0L);

- 
    Boolean/boolean result = (response) -> Optional.ofNullable(response)
                             .map(r -> r.b)
                             .map(b -> b.c)
                             .isPresent())

- 
    /* When several functions have common parts, can extract the common method (parseValueFromA) for them */

        private Long parseValueFromA(Optional<QueryResponse> response,Function<QueryResponse, Long> function) {
            return response
                .map(function)
                .orElse(null);
        }

        Long B = parseValueFromA(response, QueryResponse -> QueryResponse.B);
        Long C = parseValueFromA(response, QueryResponse -> QueryResponse.C);


---
## Sets
1. Implement `containsAny` for sets command.  
     - `Sets.intersection(set1, set2).isEmpty()`   
     - `CollectionUtils.containsAny(someCollection1, someCollection2)`
     - `setA.stream().anyMatch(setB::contains)`


---
## Data fetching handling
- **Solution 1**
```  
 A.getB().getC() 
```

- **Solution 2**
``` 
 Optional.ofNullable(A) 
    .map(A::getB())
    .map(B::getC())
    .orElseThrow(() -> new RuntimeException("C is not present!"));
```
---
## Regexp/ restrction annotation

### Integer
`@Positive` and `@PositiveOrZero`  
`@Min(100)` and  `@Max(100)`  
`@Range(min = 1000, max = 3000)`

### String
`@NotEmpty` // *String is not empty*  
`@NotNull` // *String is not Null*  
`@Size(max = 100)`  // *length of String*  
`@Pattern(regexp = "(^[1-9]$)|(^0[1-9]|1[0-2]$)")`  // *1 - 12, include 01, 02*
`@Pattern(regexp = "^\d{4}$")` // *Four digits*  
`@Pattern(regexp = "[A-Z]{3}")` // *The three character ISO 4217 currency code*

### LocalDate
`@JsonFormat(shape = JsonFormat.Shape.STRING, pattern = "yyyy-MM-dd")`

---
## Annotations
`@Data`  
`@EqualsAndHashCode(callSuper = true)` // @EqualsAndHashCode is included in @Data, and the default value of callSuper is false.

`@AvroIgnore`

---
## Functions
 - `Boolean.equals(Object obj)`
>Returns true if and only if the argument **is not null** and is a Boolean object that represents the same boolean value as this object.

- `Objects.isNull(Object A)`  
>This method is used to check if object is null or not, it doesn't check empty.

- `ObjectUtils.allNotNull(Object A, Object B,....)`
>This method is used to check if all object are not null, it doesn't check empty. 

- `StringUtils.isEmpty()`
>This method is used to check if a String object is null or **empty**. 

- `org.springframework.util.CollectionUtils.isEmpty(Object A)`    
>This method is used to check if a object is null or **empty**.

- `LocalDate.now().format(DateTimeFormatter.ofPattern("dd/MM/yyyy"))`
>To format the date.

- ` Long.MAX_VALUE`
> Get the maximum value of Long.

---
## Concepts
### final 
> A final variable can only be initialized once, it always contains the same value. If a final variable holds a reference to an object, then the state of the object may be changed by operations on the object, but the variable will always refer to the same object.

-  
        // A final class cannot be subclassed.

        public final class MyFinalClass {...}
        public class ThisIsWrong extends MyFinalClass {...} // forbidden

- 
    // A final method cannot be overridden or hidden by subclasses

        public class Base
        {
            public       void m1() {...}
            public final void m2() {...}

            public static       void m3() {...}
            public static final void m4() {...}
        }

        public class Derived extends Base
        {
            public void m1() {...}  // OK, overriding Base#m1()
            public void m2() {...}  // forbidden

            public static void m3() {...}  // OK, hiding Base#m3()
            public static void m4() {...}  // forbidden
        }

---
## Tips

### ObjectMapper
> Constructing an ObjectMapper instance is a relatively expensive operation, so it's recommended to create one object and reuse it like below. 

`private static final ObjectMapper jsonMapper = new ObjectMapper()`

### if - else   
``` 
if(x==y) {
    return a;
} else {
    return b 
}  
``` 
can be simpified as:  
`x == y ? a : b` 


### if - else if - else
  
```  
If the conditions are not based on the same thing, for example:  
if (condition A) {
    ...
}
if (condition B) {
    ...
} 
```  
  
```
If the conditions is based on the same thing, then:  
if (a > 1) {
    ...
} else if (a == 0) {
    ...
} else {
    ...
}
``` 

### if-else VS switch 
> For a **switch** statement, the **default** clause is good for error handling and testing (even it is not necessary). If it doesn't need the default clause, then **if - else** can be considered instead.

### static final VS final static
> `static final` and `final static` are the same. However `static final` is recommended by coding convention.



