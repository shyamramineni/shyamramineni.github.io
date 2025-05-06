---
title: "Dart Language Basics - Part1"
date: 2020-04-29
draft: false
tags: [ "Dart"]
---

I am learning basics of Dart programming language so that I can start developing mobile Apps using Flutter framework. This post is my notes, that I taken from reading Dart Language Tour. <!--more-->

Below is code that I written by following along Language Tour Guide

    
     main() {
      for(int i = 0; i < 5;i++){
        print('hello ${i +1}');
      }
      var number = 42;
      printInteger(number);

    
      var nameVar = "Bob";  // var defines a reference String
      dynamic nameDyn = "Bob"; // object is not single type
      String nameStr = "Bob"; // specific type
      Object nameObj = "Bob";
      print(nameVar.runtimeType); // for these .runtimeType is same
      print(nameDyn.runtimeType);
      print(nameStr.runtimeType);
      print(nameObj.runtimeType);
    
      int lineCount; //unintilized variables have value null, even numerics
      print(lineCount);
    
      final name = "Bob";
      final String nickName = "Booby";
    
      //name = "test";
      //nickName = "test";
    
      const bar = 10000;
      const double atm = 1010.98 * bar;
    
      var foo = const [];
      final barcons = const [];
    
      foo = [1,2,3];
      //barcons = [42];
    
      // Built in Types
    
      //Number
      int x = 1;
      double z = 1.2;
      print(x.toString());
      var one = int.parse('1');
    
      //String UTF-16 code unit. use single ot double quotes
      var s3 = 'It\'s easy to escapte';
      print(s3);
      var s4 = "It's easy to escapte";
      print(s4);
      var s = 'string interpolation';
      print('dart has $s');
      print('dart has ${s.toUpperCase()}');
    
      //Boolean
      bool c = true;
      var fullName = "";
      print(fullName.isEmpty);
    
      // arrays in dart are lists
      var list = [1,2,3];
      print(list.runtimeType);
      //list[3] = 4;
      list.add(4);
      print(list);
      // spread operator ...
      var list2 = [0,1, ...list];
      print(list2);
    
      //sets
      var halogens = {'fluring', 'chlorine', 'bromine', 'iodine'};
      print(halogens.runtimeType);
      halogens.add('chlorine'); // adding duplicate does give runtime err
      print(halogens);
    
      //maps
      var gifts = {
        '1' : 'biryani',
        '2' : 'icecreame',
        '3' : 'desert'
      };
      print(gifts['1']);
      gifts['4'] = 'bill';
      print(gifts.runtimeType);
      print(gifts);
    }
    
    printInteger(int aNumber) {
      print('The Number is $aNumber');
    }


