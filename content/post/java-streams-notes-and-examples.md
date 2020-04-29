---
title: "Java Streams Notes and Examples"
date: 2019-07-18T19:30:59+05:30
draft: false
tags: [ "Java", "Streams", "Collections" ]
---

This post is my notes that I collected when I was learning about Java Streams.<!--more-->

# Function Interfaces Notes
1. java.util.functions contains Functional Interfaces which provides target for lambda expressions and method references.
2. method references in Java    https://www.baeldung.com/java-method-references
3. default methods in Interface  https://www.baeldung.com/java-static-default-methods
4. static methods in Interface  https://www.baeldung.com/java-static-default-methods
5. compose functions using andThen like structures - refer to java.util.function.BiFunction functional interface code. Good example  https://www.logicbig.com/how-to/code-snippets/jcode-java-functional-interfaces-bifunction-andthen.html

# Collections and Stream
1. Stream operations map, forEach and filter are intermidaite opertions.
2. sort and collect are important functions in streams.
3. Collectors is interesting concepts for grouping, aggregation functionality.  https://www.baeldung.com/java-groupingby-collector

# Functional Interface Examples


    import java.util.function.*;
    
    public class FunctionalInterfaces {
    
        public static void main(String args[]) {
    
            Predicate<String> lengGtTen = (s) -> s.length() > 0;
            System.out.println(lengGtTen.test("20"));
    
            Consumer<String> lowerCaseConsumer = (str) -> System.out.println(str.toLowerCase());
            lowerCaseConsumer.accept("ABCD");
    
            Function<Integer,String> intToStr = (num) -> Integer.toString(num);
            System.out.println(intToStr.apply(10).length());
    
            Supplier<String> s = () -> "Back to learning Java";
            System.out.println(s.get());
    
            BinaryOperator<Integer> addTwo = (a,b) -> a + b +10;
            System.out.println(addTwo.apply(10,20));
    
            UnaryOperator<Integer> addTen = (num) -> num + 10;
            System.out.println(addTen.apply(10));
        }
    
    
    }

# Function Composing Examples


      import java.util.function.*;
      import java.lang.Runnable;
      import java.lang.Runnable;
    
      public class FunctionComposing {
    
        public static void main(String args[]) {
    
            Runnable r1 = new Runnable() {
                public void run() {
                    System.out.println(" This is r1");
                }
			};
            Runnable r2 = () -> System.out.println("This is r2");
            new Thread(r1).start();
            new Thread(r2).start();
    
            BiFunction<Integer, Integer, Integer> addFunction = (a, b) -> a + b;
            System.out.println(addFunction.apply(1, 2));
            Function<Integer, Integer> sqr = (a) -> a * a;
            BiFunction<Integer, Integer, Integer> addAndSqr = addFunction.andThen(sqr);
            System.out.println(addAndSqr.apply(2, 3));
        }
      }

# Method References

        import java.math.BigInteger;  
        import java.util.function.*;  
          
        public class MethodReferences {  
          
            public static void main(String args[]) {  
          
                IntFunction<String> tostr = Integer::toString;  
                System.out.println(tostr.apply(12345).length());  
          
                Function<String, BigInteger> strtobigint = BigInteger::new;  
                System.out.println(strtobigint.apply("234234234234"));  
          
                Consumer<String> print = System.out::print;  
                print.accept("method references");  
          
                UnaryOperator<String> appHello = "Hello "::concat;  
                System.out.print(appHello.apply("shyam"));  
          
          
            }  
       }

# Streams and Collectors Examples

    import java.util.*;  
    import java.util.stream.Collectors;  
    import java.util.stream.Stream;  
      
    public class StreamsLearning {  
      
        public static void main(String[] args) {  
      
            List<String> names = Arrays.asList("Shyam", "Suri", "Ravi", "Sharat", "Bunty");  
      
            Collections.sort(names, new Comparator<String>() {  
      
                public int compare(String a, String b) {  
                    return b.compareTo(a);  
                }  
            });  
      
            //Collections.sort(names, (String a, String b) -> b.compareTo(a));  
      
		    Collections.sort(names, (a, b) -> b.compareTo(a));  
      
            Book book1 = new Book("JK", "Harry Potter1", 50);  
            Book book2 = new Book("Thomas", "World is flat", 75);  
            Book book3 = new Book("Hit Refresh", "Satya Nadella", 80);  
            Book book4 = new Book("JK", "Harry Potter1", 50);  
      
      
            List<Book> books = Arrays.asList(book1, book2, book3, book4);  
      
            int totalCost = books.stream().collect(Collectors.summingInt(Book::getCost));  
            System.out.println(totalCost);  
      
            List<Book> books1 = Arrays.asList(book1, book2, book3, book1);  
      
            HashSet<Book> dedup = new HashSet<>(books1);  
            System.out.println(dedup);  
      
            Set<Integer> intset = new HashSet<>(Arrays.asList(1, 2, 1, 1));  
            System.out.println(intset);  
      
            Map<String, List<Book>> booksByAuthor = books.stream().collect(Collectors.groupingBy(Book::getAuthor));  
            Map<String, Integer> costBooksByAuthor = books.stream().collect(Collectors.groupingBy(Book::getAuthor, Collectors.summingInt(Book::getCost)));  
      
            System.out.println(booksByAuthor.keySet());  
            System.out.println(costBooksByAuthor);  
      
      
            Arrays.asList("red", "green", "yellow")  
                    .stream()  
                    .sorted()  
                    .findFirst()  
                    .ifPresent(System.out::println);  
      
      
            Stream.of("apple", "pear", "banana", "apricot", "cherry")  
                    .filter(fruit -> {  
                                System.out.println("filter " + fruit);  
                                return fruit.startsWith("a");  
      
                            }  
      
                    ).forEach(System.out::println);  
      
        }  
      
      
    }

