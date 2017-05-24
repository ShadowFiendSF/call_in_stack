Welcome to call in stack!

Call a function in a new stack that allocated anywhere. Do not be afraid of stack limit in your coroutines! Try to make your stack shareable between all coroutines!

```bash
#include "call_in_stack.h"
char buffer[4096];
printf(buffer, "Hello world!\n");
//Now printf run in buffer as its stack!
```

Goto https://github.com/yuanzhubi/call_in_stack/wiki/Welcome-to-call_in_stack for details.

Goto QQ Group :293767138(talk_in_stack) for further discussion.
---------------------------------------------------------------------------------------------------------------

Version 1.0.6: Important adaptive improvement for lower version of GCC!

In this version:

We add support of using call_in_stack in x64 of old GCC version ( tested since GCC 3.4),  compiled with no optimization option.
(In previous version of call_in_stack, compiling with no optimization option in x64 of old GCC version will fail to complete compile.)


---------------------------------------------------------------------------------------------------------------

Version 1.0.5: Important adaptive improvement for higher version of GCC!

In this version:

We remove __builtin_unreachable in our library because GCC has different semantic in high version(since 4.5);

We disable the -fipa-sra optimize for "do_call" function (with no performance lost because it is an assemble function indeed) in our library because it breaks the system V ABI and arguments forwarding rule.

---------------------------------------------------------------------------------------------------------------

Version 1.0.2: Now we support call_in_stack for member function.

std::string a("Hello world");
call_in_stack(printf, "%s\n", call_in_stack(from_member_fun(a, c_str))) ;

And we support call_in_stack for functor or lambda in C++11!

std::string a("Hello world");
call_in_stack_safe(buf, from_functor(
	[=](int arg){
		printf("%s\n", a.c_str());
		return arg;
	}
),2) ;

That means you can write most of your codes of function in a new stack!
