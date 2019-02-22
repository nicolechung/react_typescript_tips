# Why can't I use the type `any`?

Every once in a while, you might have to reach for the type `any`. However, you might run into a case where the use of any is forbidden.

This is because you have set `noImplicitAny` in your tsconfig to true:


```
// tsconfig.json
{
    "compilerOptions": {
        "noImplicitAny": true
    }
}
```

Setting it to false will allow you to use *any* again.