---
layout: post
title: "Comparable 와 Comparator"
date: 2020-06-24
excerpt: "Comparable 와 Comparator 인터페이스를 이용하여 객체를 정렬하는 법"
tag:
- algorithm
- Comparable
- Comparator
comments: true
---
## 객체 정렬

## Comparable
 - 정렬시 기본적으로 적용되는 기준을 정의
 - compareTo 메소드를 오버라이딩하여 기준 정의(오름차순 / 내림차순)
 - ex) Arrays.sort(array) / Collections.sort(list)

## Comparator
 - 기본 정렬 기준과 다르게 정렬하고 싶을때 사용
 - compare 메소드를 오버라이딩하여 기준 정의(오름차순 / 내림차순)
 - ex) Arrays.sort(array,comparator) / Collections.sort(list,comparator) / comparator은 Comparator인터페이스를 상속받은 클래스

## Arrays.sort 와 Collections.sort 
 - Arrays.sort : 새로 정의한 클래스에 대해서는 TimSort(Merge Sort + Insertion Sort) 사용 기본자료형에 대해서는 Dual Pivot QuickSort(Quick Sort + Insertion Sort)를 사용
 - Collections.sort : 내부적으로 Arrays.sort 사용
 
```java  
package basic;

import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;
import java.util.List;

public class Comparable_Comparator {

	static class Person implements Comparable<Person>{
		String name;
		int power;
		
		public Person(String name, int power) {
			super();
			this.name = name;
			this.power = power;
		}

		@Override
		public String toString() {
			return "Person [name=" + name + ", power=" + power + "]";
		}

		@Override
		public int compareTo(Person p) {
			// TODO Auto-generated method stub
			return this.power - p.power;
		}
		
	}
	
	//파워 순으로 정렬
	
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		
		List<Person> list = new ArrayList<>();
		list.add(new Person("임기남",1000));
		list.add(new Person("현다이",3000));
		list.add(new Person("김싸피",2000));
		System.out.println("정렬전 : "+list.toString());
		
		
		Collections.sort(list);
		System.out.println("comparable 이용 오름차순 정렬후 : "+list.toString());
		
		Collections.sort(list,new Comparator<Person>() {

			@Override
			public int compare(Person o1, Person o2) {
				// TODO Auto-generated method stub
				return o2.power-o1.power;
			}
			
		});		
		System.out.println("comparator 이용 내림차순 정렬후 : "+list.toString());
	}

}

```
## result
```

정렬전 : [Person [name=임기남, power=1000], Person [name=현다이, power=3000], Person [name=김싸피, power=2000]]
comparable 이용 오름차순 정렬후 : [Person [name=임기남, power=1000], Person [name=김싸피, power=2000], Person [name=현다이, power=3000]]
comparator 이용 내림차순 정렬후 : [Person [name=현다이, power=3000], Person [name=김싸피, power=2000], Person [name=임기남, power=1000]]

```
## Reference
 - <a href="https://gmlwjd9405.github.io/2018/09/06/java-comparable-and-comparator.html">https://gmlwjd9405.github.io/2018/09/06/java-comparable-and-comparator.html</a>
