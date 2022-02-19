# C++ Standard Concepts

## Arithmetic concepts
https://timsong-cpp.github.io/cppwp/n4868/concepts.arithmetic

```marmaid
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

##  Object concepts
https://timsong-cpp.github.io/cppwp/n4868/concepts#object

```marmaid
graph TD
    %% std::movable<T>
    is_object_v[is_object_v] --> movable([movable]);
    move_constructible([move_constructible]) --> movable;
    assignable_from1(["assignable_from&lt;T&amp;, T&gt;"]) --> movable;
    swappable([swappable]) --> movable;
    %% std::copyable<T>
    movable --> copyable;
    copy_constructible([copy_constructible]) --> copyable([copyable]);
    assignable_from2(["assignable_from&lt;T&amp;, T&amp;&gt;<br>assignable_from&lt;T&amp;, const T&amp;&gt;<br>assignable_from&lt;T&amp;, const T&gt;"]) --> copyable;
    %% std::semiregular<T>
    copyable --> semiregular([semiregular]);
    default_initializable([default_initializable]) --> semiregular;
    %% std::regular<T>
    semiregular --> regular([regular]);
    equality_comparable([equality_comparable]) --> regular;
```
