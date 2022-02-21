# C++ Standard concepts diagrams


## Concept `convertible_to`
https://timsong-cpp.github.io/cppwp/n4868/concept.convertible

```mermaid
graph TD
    %% std::convertible_to<From, To>
    is_convertible_v["is_convertible_v&lt;From, To&gt;"] --> convertible_to(["<b>convertible_to&lt;From, To&gt;</b>"]);
    AC["requires(...) {...}"] --> convertible_to;
```


## Concept `common_reference_with`
https://timsong-cpp.github.io/cppwp/n4868/concept.commonref

```mermaid
graph TD
    %% std::common_reference_with<T, U>
    same_as(["same_as&lt;COMREF(T,U), COMREF(U,T)&gt;"]) --> common_reference_with(["<b>common_reference_with&lt;T, U&gt;</b>"]);
    convertible_to(["convertible_to&lt;T, COMREF(U,T)&gt;<br>convertible_to&lt;U, COMREF(U,T)&gt;"]) --> common_reference_with;
```


## Concept `common_with`
https://timsong-cpp.github.io/cppwp/n4868/concept.common

```mermaid
graph TD
    %% std::common_with<T, U>
    same_as(["same_as&lt;CT(T,U), CT(U,T)&gt;"]) --> common_with(["<b>common_with&lt;T, U&gt;</b>"]);
    AC["requires {...}"] --> common_with;
    common_reference_with(["common_reference_with&lt;CLREF(T), CLREF(U)&gt;<br>common_reference_with&lt;CLREF(CT(T,U)), COMREF(CLREF(T),CLREF(U))&gt;"]) --> common_with;
```


## Arithmetic concepts
https://timsong-cpp.github.io/cppwp/n4868/concepts.arithmetic

```mermaid
graph TD
    %% std::integral<T>
    integral_v["integral_v&lt;T&gt;"] --> integral(["<b>integral&lt;T&gt;</b>"]);
    %% std::signed_integral<T>
    integral --> signed_integral(["<b>signed_integral&lt;T&gt;</b>"]);
    is_signed_v["is_signed_v&lt;T&gt;"] --> signed_integral;
    %% std::unsigned_integral<T>
    not_signed_v["not is_signed_v&lt;T&gt;"] --> unsigned_integral(["<b>unsigned_integral&lt;T&gt;</b>"]);
    integral --> unsigned_integral;
    %% std::floating_point<T>
    floating_point_v["floating_point_v&lt;T&gt;"] --> floating_point(["<b>floating_point&lt;T&gt;</b>"]);
```


## Concept `assignable_from`
https://timsong-cpp.github.io/cppwp/n4868/concept.assignable

```mermaid
graph TD
    %% std::assignable_from<LHS, RHS>
    AC1["is_lvalue_reference_v&lt;LHS&gt;"] --> assignable_from(["<b>assignable_from&lt;LHS, RHS&gt;</b>"]);
    common_reference_with(["common_reference_with&lt;CREF(LHS), CREF(RHS)&gt;"]) --> assignable_from;
    AC2["requires(LHS, RHS&amp;&amp;) {...}"] --> assignable_from;
```


## Concept `swappable`
https://timsong-cpp.github.io/cppwp/n4868/concept.swappable

```mermaid
graph TD
    %% std::swappable<T>
    AC1["requires(T&amp;, T&amp;) {...}"] --> swappable(["<b>swappable&lt;T&gt;</b>"]);
    %% std::swappable_with<T, U>
    common_reference_with(["common_reference_with&lt;T, U&gt;"]) --> swappable_with(["<b>swappable_with&lt;T, U&gt;</b>"]);
    AC2["requires(T&amp;&amp;, T&amp;&amp;) {...}"] --> swappable_with;
```


## Concept `destructible`
https://timsong-cpp.github.io/cppwp/n4868/concept.destructible

```mermaid
graph TD
    %% std::destructible<T>
    is_nothrow_destructible_v["is_nothrow_destructible_v&lt;T&gt;"] --> destructible(["<b>destructible&lt;T&gt;</b>"]);
```


## Concept `constructible_from`
https://timsong-cpp.github.io/cppwp/n4868/concept.constructible

```mermaid
graph TD
    %% std::constructible_from<T, Args...>
    destructible(["destructible&lt;T&gt;"]) --> constructible_from(["<b>constructible_from&lt;T, Args...&gt;</b>"]);
    is_constructible_v["is_constructible_v&lt;T, Args...&gt;"] --> constructible_from;
```


## Concept `default_initializable`
https://timsong-cpp.github.io/cppwp/n4868/concept.default.init

```mermaid
graph TD
    %% std::default_initializable<T>
    constructible_from(["constructible_from&lt;T&gt;"]) --> default_initializable(["<b>default_initializable&lt;T&gt;</b>"]);
    AC1["requires {...}"] --> default_initializable;
    AC2["<i>is-default-initializable</i>&lt;T&gt;"] --> default_initializable;
```


## Concept `move_constructible`
https://timsong-cpp.github.io/cppwp/n4868/concept.moveconstructible

```mermaid
graph TD
    %% std::move_constructible<T>
    constructible_from(["constructible_from&lt;T, T&gt;"]) --> move_constructible(["<b>move_constructible&lt;T&gt;</b>"]);
    convertible_to(["convertible_to&lt;T, T&gt;"]) --> move_constructible;
```


## Concept `copy_constructible`
https://timsong-cpp.github.io/cppwp/n4868/concept.copyconstructible

```mermaid
graph TD
    %% std::copy_constructible<T>
    move_constructible(["move_constructible&lt;T&gt;"]) --> copy_constructible(["<b>copy_constructible&lt;T&gt;</b>"]);
    constructible_from(["constructible_from&lt;T, T&amp;&gt;<br>constructible_from&lt;T, const T&amp;&gt;<br>constructible_from&lt;T, const T&gt;"]) --> copy_constructible;
    convertible_to(["convertible_to&lt;T&amp;, T&gt;<br>convertible_to&lt;const T&amp;, T&gt;<br>convertible_to&lt;const T, T&gt;"]) --> copy_constructible;
```


## Boolean testability
https://timsong-cpp.github.io/cppwp/n4868/concept.booleantestable

```mermaid
graph TD
    %% std::boolean-testable<T>
    convertible_to(["convertible_to&lt;T, bool&gt;"]) --> impl(["<i>boolean-testable-impl</i>&lt;T&gt;"]);
    impl --> boolean_testable(["<b><i>boolean-testable</i>&lt;T&gt;</b>"]);
    AC["requires(T&amp;&amp;) {...}"] --> boolean_testable;
```


## Concept `equality_comparable`
https://timsong-cpp.github.io/cppwp/n4868/concept.equalitycomparable

```mermaid
graph TD
    %% std::weakly-equality-comparable-with<T, U>
    AC["requires(CREF(T), CREF(U)) {...}"] --> wecw(["<i>weakly-equality-comparable-with</i>&lt;T, U&gt;"]);
```

```mermaid
graph TD
    %% std::equality_comparable<T>
    wecw(["<i>weakly-equality-comparable-with</i>&lt;T, T&gt;"]) --> equality_comparable(["<b>equality_comparable&lt;T&gt;</b>"]);
```

```mermaid
graph TD
    %% std::equality_comparable_with<T, U>
    equality_comparable(["equality_comparable&lt;T&gt;<br>equality_comparable&lt;U&gt;<br>equality_comparable&lt;COMREF(CREF(T), CREF(U))&gt;"]) --> equality_comparable_with(["<b>equality_comparable_with&lt;T, U&gt;</b>"]);
    common_reference_with(["common_reference_with&lt;CREF(T), CREF(U)&gt;"]) --> equality_comparable_with;
    wecw(["<i>weakly-equality-comparable-with</i>&lt;T, U&gt;"]) --> equality_comparable_with;
```


#  Concept `totally_ordered`
https://timsong-cpp.github.io/cppwp/n4868/concept.totallyordered

```mermaid
graph TD
    %% std::totally_ordered<T>
    equality_comparable(["equality_comparable&lt;T&gt;"]) --> totally_ordered(["<b>totally_ordered&lt;T&gt;</b>"]);
    pow(["<i>partially-ordered-with</i>&lt;T, T&gt;"]) --> totally_ordered;
```

```mermaid
graph TD
    %% std::totally_ordered_with<T, U>
    totally_ordered(["totally_ordered&lt;T&gt;<br>totally_ordered&lt;U&gt;<br>totally_ordered&lt;COMREF(CREF(T), CREF(U))&gt;"]) --> totally_ordered_with(["<b>totally_ordered_with&lt;T, U&gt;</b>"]);
    equality_comparable_with(["equality_comparable_with&lt;T, U&gt;"]) --> totally_ordered_with;
    pow(["<i>partially-ordered-with</i>&lt;T, U&gt;"]) --> totally_ordered_with;
```


## Object concepts
https://timsong-cpp.github.io/cppwp/n4868/concepts#object

```mermaid
graph TD
    %% std::movable<T>
    is_object_v["is_object_v&lt;T&gt;"] --> movable(["<b>movable&lt;T&gt;</b>"]);
    move_constructible(["move_constructible&lt;T&gt;"]) --> movable;
    assignable_from1(["assignable_from&lt;T&amp;, T&gt;"]) --> movable;
    swappable(["swappable&lt;T&gt;"]) --> movable;
    %% std::copyable<T>
    movable --> copyable(["<b>copyable&lt;T&gt;</b>"]);
    copy_constructible(["copy_constructible&lt;T&gt;"]) --> copyable;
    assignable_from2(["assignable_from&lt;T&amp;, T&amp;&gt;<br>assignable_from&lt;T&amp;, const T&amp;&gt;<br>assignable_from&lt;T&amp;, const T&gt;"]) --> copyable;
    %% std::semiregular<T>
    copyable --> semiregular(["<b>semiregular&lt;T&gt;</b>"]);
    default_initializable(["default_initializable&lt;T&gt;"]) --> semiregular;
    %% std::regular<T>
    semiregular --> regular(["<b>regular&lt;T&gt;</b>"]);
    equality_comparable(["equality_comparable&lt;T&gt;"]) --> regular;
```
