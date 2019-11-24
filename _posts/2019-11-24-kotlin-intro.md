---
layout: post
title: Kotlin이 무엇이죠? 먹는건가요?
featured-img: kotlin-intro
categories: [Kotlin]
---

# 코틀린 너 누구냐?

## 탄생
2011년 [JetBrains](https://www.jetbrains.com/)에서 공개되었다.

## 소개
Kotlin은 JVM 기반의 언어이며 세미콜론은 옵션이다.
또한 Java와 상호운용이 100% 지원된다!
JVM bytecode가 기본이지만 Kotlin/Native Compiler를 통해 최종적으로는 기계어로 Compile이 가능하다.

## 특징
1. Java보다 훨씬 간결한 문법을 제공하면서 런타임 오버헤드가 거의 없다.
2. 오버헤드 없는 Null 안정성을 제공한다.
3. 강제하지 않는 예외처리.
4. 모든 함수가 값을 가진다.
5. Java의 Integer, Double처럼 primitive type을 위한 별도의 wrapper class가 존재하지 않는다. 모든 primitive type은 객체 취급을 받는다.
6. 확장함수, 연산자 오버로딩을 지원한다.
7. static method가 없다. companion object를 사용해 감싸야 한다.
8. Java 6에 호환된다.
9. Java와의 상호 운용이 100% 지원된다.

## 간결한 코드

### in과 Range문
```Kotlin
val i = 5
println(i in 1..10) // true

for (i in 0..10 step 3) print("$i ") // 0 3 6 9 출력
for (i in 10 downTo 0 step 2) print("$i ") // 10 8 6 4 2 0 출력

// 한자릿수 출력
print(
    when (i) {
        !in 1..9 step 2 -> "홀수 아님"
        in 0..9 -> "한자릿수"
        else -> "otherwise"
    }
)
```

### is 연산자
```Kotlin
npcContainer.forEach { npc ->
    if (npc is Visible) npc.drawBody(gc, g) // npc가 Visible형으로 자동 변환되었다.
    if (npc is Glowing) npc.drawGlow(gc, g) // npc가 Glowing형으로 자동 변환되었다.
}

when (expr) {
    is Num -> expr.value // expr이 Num형으로 자동 변환되었다.
    is Sum -> eval(expr.left) + eval(expr.right) // expr이 Sum형으로 자동 변환되었다.
    else -> throw IllegalArgumentException("퉤에엣")
}
```

### if식
if문이 식으로 표현된다.
```Kotlin
print(if (Random.nextBoolean()) "TRUE" else "FALSE") // 둘중에 하나 출력
```

## 안전성
오류 방지로 null-safe 연산자를 쓸 수 있다. (ex. s as String?)
안전한 형변환 키워드인 as? 가 존재한다. (ex. s as? String)
```Kotlin
/*
null이거나 null은 아니지만 대상 타입으로 형변환될 수 없는 경우와 같은
형변환이 실패하는 모든 경우에 대해 안전하게 null을 반환해준다.
*/
null as? String // null
"string" as? File // null

/*
반면 as는 경우에 따라 kotlin.TypeCastException이나
java.lang.ClassCastException 예외를 발생시킬 수 있다
*/
null as File // kotlin.TypeCastException 예외 발생
null as File? // null
"string" as File // java.lang.ClassCastException 예외 발생
"string" as File? // java.lang.ClassCastException 예외 발생
```