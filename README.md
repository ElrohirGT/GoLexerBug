# Go Array Access Bug

## Reproduce the bug

1. Use `nix develop` to get access to the same compiler version as when this bug
   was discovered.
1. Run the program with a debugger: `gdlv debug ./bug input`.
1. Watch closely the access to the `rule` variable defined on line 406.

## Description of the bug
On the Lexer file I'm creating a `rule` variable.
https://github.com/ElrohirGT/GoLexerBug/blob/a05cb3881541bf409148fa4bbec95c77f47b2a47/lex.go#L404-L407

When I inspect the value of this variable with a debugger I can see that the index and the value returned do not match!
For example in the image below, I'm accessing the rule with the index 2 but the `rule` variable only default values!

![image](https://github.com/user-attachments/assets/1f23496a-292e-49b1-a4c4-51a8fa351db7)

Later in the execution of the program, the index is 1 but the `rule` variable acts as if the index was actually 2!

![image](https://github.com/user-attachments/assets/5935ca3f-9e90-45db-b114-231a1faeb661)

## Context of the bug
I'm doing a Compiler generator similar to Yalecc, the lexer.go file is the generated code of my compiler generator for a very simple grammar, this issue is honestly driving me insane.

## Found workaround
For some reason the bug only manifests if I create the intermediate variable `rule`. If instead I type the complete access on the map everytime, it works as expected!
Test it out with the fixed.go package
