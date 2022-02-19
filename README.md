# C++ Standard Concepts


## Arithmetic concepts
https://timsong-cpp.github.io/cppwp/n4868/concepts.arithmetic

```mermaid
graph TD
    %% std::integral<T>
    integral_v[integral_v] --> integral([integral]);
    %% std::signed_integral<T>
    integral --> signed_integral([signed_integral]);
    is_signed_v[is_signed_v] --> signed_integral;
    %% std::unsigned_integral<T>
    not_signed_v[!is_signed_v] --> unsigned_integral([unsigned_integral]);
    integral --> unsigned_integral;
    %% std::floating_point<T>
    floating_point_v[floating_point_v] --> floating_point([floating_point])
```


## Concept `destructible`
https://timsong-cpp.github.io/cppwp/n4868/concept.destructible

```mermaid
graph TD
    %% std::destructible<T>
    is_nothrow_destructible_v["is_nothrow_destructible_v&lt;T&gt;"] --> destructible(["destructible&lt;T&gt;"]);
```


## Concept `constructible_from`
https://timsong-cpp.github.io/cppwp/n4868/concept.constructible

```mermaid
graph TD
    %% std::constructible_from<T, Args...>
    destructible(["destructible&lt;T&gt;"]) --> constructible_from(["constructible_from&lt;T, Args...&gt;"]);
    is_constructible_v["is_constructible_v&lt;T, Args...&gt;"] --> constructible_from;
```


## Concept `default_initializable`
https://timsong-cpp.github.io/cppwp/n4868/concept.default.init

```mermaid
graph TD
    %% std::default_initializable<T>
    constructible_from(["constructible_from&lt;T&gt;"]) --> default_initializable(["default_initializable&lt;T&gt;"]);
    AC1["requires{ T{}; }"] --> default_initializable;
    AC2["<i>is-default-initializable</i>&lt;T&gt;"] --> default_initializable;
```


## Concept `move_constructible`
https://timsong-cpp.github.io/cppwp/n4868/concept.moveconstructible

```mermaid
graph TD
    %% std::move_constructible<T>
    constructible_from(["constructible_from&lt;T, T&gt;"]) --> move_constructible(["move_constructible&lt;T&gt;"]);
    convertible_to(["convertible_to&lt;T, T&gt;"]) --> move_constructible;
```


## Concept `copy_constructible`
https://timsong-cpp.github.io/cppwp/n4868/concept.copyconstructible

```mermaid
graph TD
    %% std::copy_constructible<T>
    move_constructible(["copy_constructible&lt;T&gt;"]) --> copy_constructible(["copy_constructible&lt;T&gt;"]);
    constructible_from(["constructible_from&lt;T, T&amp;&gt;<br>constructible_from&lt;T, const T&amp;&gt;<br>constructible_from&lt;T, const T&gt;"]) --> copy_constructible;
    convertible_to(["convertible_to&lt;T&amp;, T&gt;<br>convertible_to&lt;const T&amp;, T&gt;<br>convertible_to&lt;const T, T&gt;"]) --> copy_constructible;
```


## Boolean testability
https://timsong-cpp.github.io/cppwp/n4868/concept.booleantestable

```mermaid
graph TD
    %% std::boolean-testable<T>
    convertible_to(["convertible_to&lt;T, bool&gt;"]) --> impl(["<i>boolean-testable-impl</i>&lt;T&gt;"]);
    impl --> boolean_testable(["<i>boolean-testable</i>&lt;T&gt;"]);
    AC["requires (T&amp;&amp;) {...}"] --> boolean_testable;
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
    wecw(["<i>weakly-equality-comparable-with</i>&lt;T, T&gt;"]) --> equality_comparable(["equality_comparable&lt;T&gt;"]);
```

```mermaid
graph TD
    %% std::equality_comparable_with<T, U>
    equality_comparable(["equality_comparable&lt;T&gt;<br>equality_comparable&lt;U&gt;<br>equality_comparable&lt;COMREF(CREF(T), CREF(U))&gt;"]) --> equality_comparable_with(["equality_comparable_with&lt;T, U&gt;"]);
    common_reference_with(["common_reference_with&lt;CREF(T), CREF(U)&gt;"]) --> equality_comparable_with;
    wecw(["<i>weakly-equality-comparable-with</i>&lt;T, U&gt;"]) --> equality_comparable_with;
```


#  Concept `totally_ordered`
https://timsong-cpp.github.io/cppwp/n4868/concept.totallyordered

```mermaid
graph TD
    %% std::totally_ordered<T>
    equality_comparable(["equality_comparable&lt;T&gt;"]) --> totally_ordered(["totally_ordered&lt;T&gt;"]);
    pow(["<i>partially-ordered-with</i>&lt;T, T&gt;"]) --> totally_ordered;
```

```mermaid
graph TD
    %% std::totally_ordered_with<T, U>
    totally_ordered(["totally_ordered&lt;T&gt;<br>totally_ordered&lt;U&gt;<br>totally_ordered&lt;COMREF(CREF(T), CREF(U))&gt;"]) --> totally_ordered_with(["totally_ordered_with&lt;T, U&gt;"]);
    equality_comparable_with(["equality_comparable_with&lt;T, U&gt;"]) --> totally_ordered_with;
    pow(["<i>partially-ordered-with</i>&lt;T, U&gt;"]) --> totally_ordered_with;
```


## Object concepts
https://timsong-cpp.github.io/cppwp/n4868/concepts#object

```mermaid
graph TD
    %% std::movable<T>
    is_object_v["is_object_v&lt;T&gt;"] --> movable(["movable&lt;T&gt;"]);
    move_constructible(["move_constructible&lt;T&gt;"]) --> movable;
    assignable_from1(["assignable_from&lt;T&amp;, T&gt;"]) --> movable;
    swappable(["swappable&lt;T&gt;"]) --> movable;
    %% std::copyable<T>
    movable --> copyable(["copyable&lt;T&gt;"]);
    copy_constructible(["copy_constructible&lt;T&gt;"]) --> copyable;
    assignable_from2(["assignable_from&lt;T&amp;, T&amp;&gt;<br>assignable_from&lt;T&amp;, const T&amp;&gt;<br>assignable_from&lt;T&amp;, const T&gt;"]) --> copyable;
    %% std::semiregular<T>
    copyable --> semiregular(["semiregular&lt;T&gt;"]);
    default_initializable(["default_initializable&lt;T&gt;"]) --> semiregular;
    %% std::regular<T>
    semiregular --> regular(["regular&lt;T&gt;"]);
    equality_comparable(["equality_comparable&lt;T&gt;"]) --> regular;
```
