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
## Sets / List
- Implement `containsAny` for sets command.  
     - `Sets.intersection(set1, set2).isEmpty()`   
     - `CollectionUtils.containsAny(someCollection1, someCollection2)`
     - `setA.stream().anyMatch(setB::contains)`


- To a set  

        Set<String> orderedItems = orderedItemsSet.stream()
            .map(str -> str.replaceAll("\\s",""))
            .map(String::toLowerCase)
            .collect(Collectors.toSet())

- Return empty list/value

    - return empty list     

            var orderLines = Optional.ofNullable(request.getStudents())
                    .map(Students::getStudents)
                    .orElse(Collections.emptyList())

    - Return empty value
  
            var student = Optional.ofNullable(request.getStudent()).orElse(null)


---
## Validator

- Validate configuration of YAML file   
  
        xxxx-config :
        settings :
            normal :
            - level1: 175_00
                reward: 510
            - level2: 350_00
                reward: 530
            high :
            - level1: 175_00
                reward: 550
            - level2: 350_00
                reward: 580
        userMppingList :
            DEFAULT   : normal  #Default is mandatory to be set
            USER12345 : high    
        ========================================================================= 
        @Override
        public boolean supports(@NotNull Class<?> clazz) {
            return XxxxConfiguration.class.isAssignableFrom(clazz);
        }  
        @Override
        public void validate(@NotNull Object target, @NotNull Errors errors) {
            XxxxConfiguration config = (XxxxConfiguration) target;
            if (isNull(config.getSettings())) {
                errors.rejectValue("settings", "settings", "Setting is null");
            } else if (getUserMppingList() == null) {
                errors.rejectValue("userMppingList", "userMppingList", "userMppingList is null");
            } else if (!config.getSetting().containsKey(getUserMppingList().get(DEFAULT))) {
                errors.rejectValue("settings", "settings", "Default setting not defined");
            }
        }

- Assert 
> Java also provides a second syntax for assertions that takes a string, which will be used to construct the AssertionError if one is thrown:  

        public void setup() {
            Connection conn = getConnection();
            // or assert conn != null;
            assert conn != null : "Connection is null";
        }

___
## Exceptions

- message throw check
  
        def ex = thrown(IllegalArgumentException)
        ex.message == "(java.lang.IllegalArgumentException: XXX)

---
## Data fetching handling
- Solution 1
  
    `A.getB().getC()` 

- Solution 2

        Optional.ofNullable(A) 
            .map(A::getB())
            .map(B::getC())
            .orElseThrow(() -> new RuntimeException("C is not present!"));

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

### static
> In the Java programming language, the keyword static indicates that the particular member belongs to a type itself, rather than to an instance of that type.  
This means that only one instance of that static member is created which is shared across all instances of the class.  
It doesn't matter how many times we initialize a class; there will always be only one copy of static field belonging to it. The value of this static field will be shared across all object of either same of any different class.

### Race condition
> A race condition occurs when two or more threads can access shared data and they try to change it at the same time. Because the thread scheduling algorithm can swap between threads at any time, you don't know the order in which the threads will attempt to access the shared data. Therefore, the result of the change in data is dependent on the thread scheduling algorithm, i.e. both threads are "racing" to access/change the data.

    if (x == 5) // The "Check"
    {
        y = x * 2; // The "Act"

        // If another thread changed x in between "if (x == 5)" and "y = x * 2" above,
        // y will not be equal to 10.
    }

---
## Tips

### ObjectMapper
> Constructing an ObjectMapper instance is a relatively expensive operation, so it's recommended to create one object and reuse it like below. 

`private static final ObjectMapper jsonMapper = new ObjectMapper()`

- Log values as a JSON
 
        log.info(
            "Log info",
            value("log_name", log_name),
            value("log_type", log_type),
            value("log_variables", jsonMapper.writeValueAsString(localVariable))
        );

- Two ways to set PropertyNamingStrategy be SNAKE_CASE
 
        spring:
            jackson:
                property-naming-strategy: SNAKE_CASE  
        ==========================================================
        @Configuration
        public class JacksonConfiguration {

            @Bean
            public Jackson2ObjectMapperBuilder jackson2ObjectMapperBuilder() {
                return new Jackson2ObjectMapperBuilder()
                        .propertyNamingStrategy(PropertyNamingStrategy.SNAKE_CASE);
                // insert other configurations
            }

        } 

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


## Other

### Checked / Unchecked assignment
Checked assignment: `Map<String, Object> factMap = new HashMap<>()`  
Unchecked assignment: `Map<String, Object> factMap = new HashMap()`

