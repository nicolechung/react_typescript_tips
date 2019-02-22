# Why is my build so slow?

Typescript React projects can be very slow with your fans whirring a lot.

This is often because your build / development is a multi-step process:

Typescript ->
Compile with the Typescript compiler into JS ->
Transpile with Babel into JS

The reason a lot of projects were stuck (historically) with this additional Babel step is that a lot of React projects use Babel plugins, and for a Typescript project to take advantage of this, the Babel transpiler was used.

The good news is, you don't have to do this anymore. You can skip using the Typescript compiler and just use Babel 7 now!

[Typescript with Babel] (https://iamturns.com/typescript-babel/)
[React Styled components Typescript Starter] (https://github.com/JinSY/React-Styled-TypeScript-Starter)